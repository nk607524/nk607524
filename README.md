#pragma once

#include <QWidget>
#include <QtWidgets>
#include <QMainWindow>
#include "TubeFREPropertiesWidget.h"
#include <QToolBox>
#include "ui_TubeFREPropertiesWidget.h"
#include "Flow_Area.h"
#include "Friction_Factor.h"
#include "Heat_Transfer.h"
#include "Variation.h"
#include "Goal_Seeking.h"

#include <QToolBox>



class TubeFREPropertiesWidget : public QWidget
{
	Q_OBJECT

public:

	TubeFREPropertiesWidget(QWidget *parent = nullptr);
	~TubeFREPropertiesWidget();
	void on_toolBox_currentChanged(int index);

private:
	Ui::TubeFREPropertiesWidgetClass ui;
	
	/*void setupToolBox();*/

	
};












#include "TubeFREPropertiesWidget.h"



TubeFREPropertiesWidget::TubeFREPropertiesWidget(QWidget *parent)
	: QWidget(parent)
{
	ui.setupUi(this);

    /*setupToolBox();
   */
	
}


	




TubeFREPropertiesWidget::~TubeFREPropertiesWidget()
{}

//void TubeFREPropertiesWidget::setupToolBox()
////{
////    QWidget* flowAreaWidget = new Flow_Area();
////    QWidget* frictionFactorWidget = new Friction_Factor();
////    QWidget* heatTransferWidget = new Heat_Transfer();
////    QWidget* variationWidget = new Variation();
////    QWidget* goalSeekingWidget = new Goal_Seeking();
////
////    // Add widgets to the QToolBox
////    ui.toolBox->addItem(flowAreaWidget, "Flow Area");
////    ui.toolBox->addItem(frictionFactorWidget, "Friction Factor");
////    ui.toolBox->addItem(heatTransferWidget, "Heat Transfer");
////    ui.toolBox->addItem(variationWidget, "Variation");
////    ui.toolBox->addItem(goalSeekingWidget, "Goal Seeking");
////
////
//
//}



void TubeFREPropertiesWidget::on_toolBox_currentChanged(int index)
{

    Flow_Area* flow = new Flow_Area();

    if (index == 1)
    {
        flow->show();
    }

}











#pragma once

#include <QWidget>
#include "ui_Flow_Area.h"
#include "Flow_Area.h"
#include "TubeFREPropertiesWidget.h"

class Flow_Area : public QWidget
{
	Q_OBJECT

public:
	Flow_Area(QWidget *parent = nullptr);
	~Flow_Area();

private:
	Ui::Flow_AreaClass ui;
};




#include "Flow_Area.h"

Flow_Area::Flow_Area(QWidget *parent)
	: QWidget(parent)
{
	ui.setupUi(this);
}

Flow_Area::~Flow_Area()
{}










