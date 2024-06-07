#pragma once

#include <QWidget>
#include "ui_BCManagementMainWidget.h"
#include "BCMTableTabWidget.h"
#include "BCMBCScalingTabWidget.h"
#include "BCMScalingGroupTabWidget.h"
#include "BCMImportedDataTabWidget.h"

#include <BCManagementController.h>

class BCManagementMainWidget : public QWidget
{
	Q_OBJECT

public:
	BCManagementMainWidget(QWidget *parent = nullptr);
	~BCManagementMainWidget();
public slots:
	void tabChanged(int p_newIndex);
	void tabClicked(int p_newIndex);
	void bttnApplyChangesClicked();
	void closeRequested();
protected:
	void UpdateViewModel(int p_iTabIndex);
	void RevertViewModel(int p_iTabIndex);

	Ptr(CBCManagementController)	m_pBCMgmtCtrl;

private:
	Ui::BCManagementMainWidgetClass ui;

	//m_prevIndex is used to get the previous tab when changing the current tab
	int m_prevIndex;

	//flag to ignore change signal
	bool m_bIgnoreChangeSignal = false;

	BCMTableTabWidget* bcTableTab;
	BCMBCScalingTabWidget* bcScalingTab;
	BCMScalingGroupTabWidget* scalingGroupTab;
	BCMImportedDataTabWidget* importedDataTab;
};
