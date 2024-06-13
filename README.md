#pragma once

#include <QtWidgets>
#include <QMainWindow>
#include "ui_QtVNetMainWindow.h"
#include "QtSceneView.h"
#include "QtVNetModes.h"
#include "VNetQtWindowManagement.h"

#ifndef __VNet_1_0SceneViewController_HeaderFile__
#include <VNet_1_0SceneViewController.h>
#endif //__VNet_1_0ViewController_HeaderFile__

#ifndef __Ptr_VNet_1_0SceneViewController_HeaderFile__
#include <Ptr_VNet_1_0SceneViewController.h>
#endif


class QtVNetMainWindow  : public QMainWindow
{
	Q_OBJECT

public:
	static QtVNetMainWindow* getInstance(Ptr(CVNet_1_0AppController) p_AppCtrl = NULL);
	
	~QtVNetMainWindow();


	void setCurrentViewPath(Ptr(CVNet_1_0AppController) p_AppCtrl, TCollection_AsciiString p_strViewPath);
	TCollection_AsciiString getCurrentViewPath() { return m_strViewPath; }

	void DestroyFlwWnds();
	void CreateFlwWnds();

public slots:
	
	void launchSceneWizard();
	void launchBCManagement();
	

protected:
	QtVNetMainWindow(QWidget *parent = 0);

	virtual void closeEvent(QCloseEvent* event) override;
	void createActions();

	static QtVNetMainWindow* instance;

private:
	
	QtVNetModes* m_VnetMode;
	VNetQtWindowManagement* m_VnetWinMan;
	ads::CDockManager* m_DockManager;

	Ui::QtVNetMainWindowClass ui;
	//temp variables
	Ptr(CVNet_1_0AppController) m_AppCtrl;
	TCollection_AsciiString m_strViewPath;
};









#include "QtVNetMainWindow.h"
#include "VNET_2_0_GUI.h"
#include "SceneWizardMainWidget.h"
#include "BCManagementMainWidget.h"
#include "RibbonTab.h"
#include "FlowWidget.h"

#include "QtVNetSaveManager.h"
#include <QDebug>

#include <iostream>

#include <QTime>
#include <QLabel>
#include <QTextEdit>
#include <QCalendarWidget>
#include <QFrame>
#include <QTreeView>
#include <QFileSystemModel>
#include <QBoxLayout>
#include <QSettings>
#include <QDockWidget>
#include <QDebug>
#include <QResizeEvent>
#include <QAction>
#include <QWidgetAction>
#include <QComboBox>
#include <QInputDialog>
#include <QRubberBand>
#include <QPlainTextEdit>
#include <QTableWidget>
#include <QScreen>
#include <QStyle>
#include <QMessageBox>
#include <QMenu>
#include <QToolButton>
#include <QToolBar>
#include <QPointer>
#include <QMap>
#include <QElapsedTimer>
#include "Vnet_2_0_Util.h"

QtVNetMainWindow*	QtVNetMainWindow::instance = nullptr;

QtVNetMainWindow* QtVNetMainWindow::getInstance(Ptr(CVNet_1_0AppController) p_AppCtrl)
{
	if (instance == nullptr )
	{
		//Raise_If_NULL_SMART_PTR(p_AppCtrl, "QtVNetMainWindow::getInstance");
		instance = new QtVNetMainWindow();
		instance->m_AppCtrl = p_AppCtrl;
	}
	return instance;
}

QtVNetMainWindow::QtVNetMainWindow(QWidget *parent)
	: QMainWindow(parent)
{
	ui.setupUi(this);
	createActions();

	m_VnetWinMan = VNetQtWindowManagement::getInstance(this);
	m_VnetMode = QtVNetModes::getInstance();

	
	//m_VnetWinMan->getRibbonWidget();

	//setCentralWidget(new QMdiArea(this));
	//setDockNestingEnabled(true);
	//
	//Adding Ribbon tab
	//QDockWidget* ribbonDock = new QDockWidget("", this);
	//RibbonTab* tabRibbon = new RibbonTab(ribbonDock);
	//ribbonDock->setWidget(tabRibbon);
	//ribbonDock->setAllowedAreas(Qt::TopDockWidgetArea);
	//addDockWidget(Qt::TopDockWidgetArea,ribbonDock);
	//ribbonDock->setFeatures(ribbonDock->features() & ~QDockWidget::DockWidgetClosable);
	//ribbonDock->setFloating(false);
	//QWidget* titleWidget = new QWidget(this); /* where this a QMainWindow object */
	//ribbonDock->setTitleBarWidget(titleWidget);
	//ribbonDock->show();

	////Adding Flow Widget
	//QDockWidget* flowDock = new QDockWidget("", this);
	//FlowWidget* flowWidget = new FlowWidget(flowDock);
	//flowDock->setWidget(flowWidget);
	//flowDock->setAllowedAreas(Qt::LeftDockWidgetArea);
	//addDockWidget(Qt::LeftDockWidgetArea, flowDock);
	//flowDock->setFeatures(flowDock->features() & ~QDockWidget::DockWidgetClosable);
	//flowDock->setFloating(false);
	//flowDock->setTitleBarWidget(new QWidget(this));
	//flowDock->show();
	//VNetQtWindowManagement::getInstance()->setFlowWidget(flowWidget);

	
	
	connect(ui.actionScene_Wizard, SIGNAL(triggered()), this,SLOT(launchSceneWizard()) );
	QMetaObject::Connection l_conn = connect(ui.actionOpen, SIGNAL(triggered()), static_cast<VNET_2_0_GUI*>(qApp)/*qobject_cast<VNET_2_0_GUI*>(VNET_2_0_GUI::instance())*/, SLOT(onFileOpen()));
	connect(ui.actionClose, SIGNAL(triggered()), static_cast<VNET_2_0_GUI*>(qApp)/*qobject_cast<VNET_2_0_GUI*>(VNET_2_0_GUI::instance())*/, SLOT(OnCloseProject()));
	connect(ui.actionBoundary_Condition_Management, SIGNAL(triggered()), this, SLOT(launchBCManagement()));
}

void QtVNetMainWindow::closeEvent(QCloseEvent * event)
{
	Ptr(CVNet_1_0AppController) l_pAppCtrl = CVNet_1_0AppController::GetAppController();
	TCollection_AsciiString l_strProjectPath = l_pAppCtrl->GetProjectPath();
	TCollection_AsciiString l_strProjectName = l_pAppCtrl->GetProjectName();
	if (QtVNetSaveManager::CloseCurrentProject(true) != IDCANCEL)
	{
		if (l_strProjectPath != "" && l_strProjectName != "")
			l_pAppCtrl->RemoveBackupData(l_strProjectPath, l_strProjectName);
		//CMDIFrameWnd::OnClose();
	}
	VNetQtWindowManagement::releaseInstance();
	QtVNetModes::releaseInstance();
	m_VnetWinMan = nullptr;
	m_VnetMode = nullptr;
	QMainWindow::closeEvent(event);
}

void QtVNetMainWindow::createActions()
{
	ui.toolBar->addAction(ui.actionOpen);
	ui.toolBar->setToolButtonStyle(Qt::ToolButtonTextUnderIcon);
	ui.actionOpen->setIcon(Vnet_2_0_Util::svgIcon(":/VNET_2_0_GUI/icons/file_open_black_24dp.svg"));
	ui.toolBar->addSeparator();

	ui.toolBar->addAction(ui.actionBoundary_Condition_Management);
	ui.actionBoundary_Condition_Management->setIcon(Vnet_2_0_Util::svgIcon(":/VNET_2_0_GUI/icons/dashboard_black_24dp.svg"));

	ui.toolBar->addSeparator();

	ui.toolBar->addAction(ui.actionScene_Wizard);
	ui.actionScene_Wizard->setIcon(Vnet_2_0_Util::svgIcon(":/VNET_2_0_GUI/icons/collections_black_24dp.svg"));
}

QtVNetMainWindow::~QtVNetMainWindow()
{

}

void QtVNetMainWindow::setCurrentViewPath(Ptr(CVNet_1_0AppController) p_AppCtrl, TCollection_AsciiString p_strViewPath)
{
	m_AppCtrl = p_AppCtrl;
	m_strViewPath = p_strViewPath;
}

void QtVNetMainWindow::DestroyFlwWnds()
{
}

void QtVNetMainWindow::CreateFlwWnds()
{
}

void QtVNetMainWindow::launchSceneWizard()
{
	if (!QtVNetModes::getInstance()->IsProjMenuEnabled())
	{
		QMessageBox::critical(this, "Error", "Project is not open or another module is open.");
		return;
	}
	if (!(QtVNetModes::getInstance()->isVNetModeEnabled(QtVNetModes::VNetMode::SCENE_WIZARD_MODE)))
	{
		VNetQtWindowManagement::getInstance()->openDockWidget(new SceneWizardMainWidget(), "Scene Wizard", QtVNetModes::VNetMode::SCENE_WIZARD_MODE);
	}
	else
	{
		QMessageBox::information(this, "Error", "Scene Wizard is already running");
	}


}

void QtVNetMainWindow::launchBCManagement()
{
	QWidget* widget = VNetQtWindowManagement::getInstance()->getDockWidget(QString(BCM_MAIN_WIDGET));
	if (widget != nullptr)
	{
		ads::CDockWidget* DockWidget =qobject_cast<ads::CDockWidget*>((widget->parent()));
		DockWidget->toggleView();
		return;
	}
	if (!QtVNetModes::getInstance()->IsProjMenuEnabled())
	{
		QMessageBox::critical(this, "Error", "Project is not open or another module is open.");
		return;
	}

	VNetQtWindowManagement::getInstance()->openDockWidget(new BCManagementMainWidget(), "Boundary Condition Management", QtVNetModes::VNetMode::BC_MANGEMENT_MODE);
}
