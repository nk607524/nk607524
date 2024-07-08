#pragma once

#include <QWidget>
#include "ui_Flow_Area.h"
#include "Flow_Area.h"



class Flow_Area : public QWidget
{
	Q_OBJECT

public:
	enum Mode {
		FRE,
		EditMeter
		
	};

	/*enum ComboBoxOption {
		StandardDrillSize = 0,
		StandardTube = 1
	};*/
	Flow_Area(QWidget *parent = nullptr);
	~Flow_Area();
	
	int Ind;
	void setMode(Mode mode);///FRe,miter bend//Tubepropertieswidget,editmeterbendcharacterstics

	//void setupComboBox();
	
public slots:
	void showarea();
	void miterbend();
	//void onComboBoxIndexChanged(int index);


private:

	Ui::Flow_AreaClass ui;

	   Mode currentMode;     ///it was for enum mode 

};















#include "Flow_Area.h"

Flow_Area::Flow_Area(QWidget* parent)
    : QWidget(parent)
{
    ui.setupUi(this);
    connect(ui.comboBox, SIGNAL(activated(int)), this, SLOT(miterbend()));


}

Flow_Area::~Flow_Area()
{}

void Flow_Area::setMode(Mode mode)
{
    currentMode = mode;
    ui.comboBox->clear();
    if (mode == FRE) {
        ui.comboBox->addItem("Standard Drill Size");
        ui.comboBox->addItem("Circular");

        ui.comboBox->addItem("Axial Gap");
        ui.comboBox->addItem("Radial Gap, Do");
        ui.comboBox->addItem("Radial Gap, Di");
        ui.comboBox->addItem("Radial Gap, Davg");
        ui.comboBox->addItem("Annulus");
        ui.comboBox->addItem("Rectangle");
        ui.comboBox->addItem("Square");
        ui.comboBox->addItem("Round Slot, C-C");
        ui.comboBox->addItem("Round slot,E-E");
        ui.comboBox->addItem("Ellipse");
        ui.comboBox->addItem("Semi Circle");
        ui.comboBox->addItem("Circular Sector");
        ui.comboBox->addItem("Right Triangle");
        ui.comboBox->addItem("Isosceles Triangle");
        ui.comboBox->addItem("Dh, Perimeter");
        ui.comboBox->addItem("Dh, Area");
        ui.comboBox->addItem("Perimeter, Area");
        ui.comboBox->addItem("Perimeter, De");
        ui.comboBox->addItem("Geometric Area");
        ui.comboBox->addItem("Effective Area");


        // Add other FRE items here...
    }
    else if (mode == EditMeter) {
        // Add other EditMeter items here...

    ui.comboBox->addItem("Standard Tube");
    ui.comboBox->addItem("Non-Standard Tube");
    ui.comboBox->addItem("Circular,Do,Tw");
    ui.comboBox->addItem("Circular,Di");
    ui.comboBox->addItem("Annulus");
    ui.comboBox->addItem("Round Slot,C-C");
    ui.comboBox->addItem("Round Slot,E-E");
    ui.comboBox->addItem("Ellipse");
    ui.comboBox->addItem("Rectangle");
    ui.comboBox->addItem("Square");
    ui.comboBox->addItem("Dh, Perimeter");
    ui.comboBox->addItem("Dh, Area");
    ui.comboBox->addItem("Perimeter, Area");
    ui.comboBox->addItem("Perimeter, De");
    }
        miterbend();

}

void Flow_Area::showarea()
{
    ui.comboBox->show();
    ui.comboBox_2->show();
    ui.comboBox_3->show();
    ui.lineEdit->show();
    ui.lineEdit_2->show();
    ui.lineEdit_3->show();
    ui.lineEdit_4->show();
    ui.lineEdit_5->show();
    ui.lineEdit_6->show();
    ui.lineEdit_7->show();
}

void Flow_Area::miterbend()
{
    Ind = ui.comboBox->currentIndex();
    if (currentMode == EditMeter)
    {
        // Add other cases for FRE items here...
        switch (Ind)
        {
        case 0: // Standard Tube
            showarea();
            ui.comboBox_2->clear();
            ui.comboBox_2->addItem("0.5000");
            ui.label_2->setText("Diameter Outer\n    (in)");
            ui.lineEdit->hide();
            ui.label_3->setText("Thickness Wall\n  (in)");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");
            ui.comboBox_3->hide();
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 1: // Non-Standard Tube
            showarea();
            ui.comboBox_2->clear();
            ui.comboBox_2->addItem("0.5000");
            ui.label_2->setText("Diameter Outer\n    (in)");
            ui.lineEdit->hide();
            ui.comboBox_3->clear();
            ui.comboBox_3->addItem(" ");
            ui.label_3->setText("Thickness Wall\n  (in)");
            ui.lineEdit_2->hide();
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 2: // Circular, Do, Tw
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter Outer\n    (in)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Thickness Wall\n  (in)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: white;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 3: // Circular, Di
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter Inner\n    (in)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Thickness Wall\n  (in)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: grey;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 4: // Annulus
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter Outer\n    (in)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Diameter Inner\n  (in)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: white;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 5: // Round Slot, C-C
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter Outer\n    (in)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Distance\nC-C (in)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: white;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
           
        case 6:  //Round Slot E-E
            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText("Width (inches)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Length\n  (inches)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: white;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;

        case 7:  //Ellipase
            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText("Major Diameter\n (in)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Minor Diameter\n  (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: white;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;

        case 8:  //Rectangle

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText("Width (inches)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Length\n  (inches)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: white;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;

        case 9:  //Square 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText("side (inches)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent\n  Radius(in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;

        case 10:  //Dh, Peerimeter 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: white;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: white;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;


        case 11:  //Dh, Area 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: white;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: white;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;

        case 12:  // Peerimeter  Area

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: white;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: white;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;


        case 13:  // Perimeter, DE

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: white;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: white;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color:grey ;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;




            
           
   





        }



                

      

    }
    else if (currentMode == FRE)
 {
        switch (Ind)
        {
        case 0: // Standard drill size
            showarea();
            ui.comboBox_2->clear();
            ui.comboBox_2->addItem(" ");
            ui.label_2->setText("Diameter inches\n    (in)");
            ui.lineEdit->hide();
            ui.label_3->setText("Drill Set");
            ui.lineEdit_2->hide();
            ui.comboBox_3->addItem(" ");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 1: // circular 
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter \n    (inches)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Radius \n  (inches)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: grey;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            
            break;
        case 2: // Axial Gap
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter \n    (inches)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Axial Gap\n  (inches)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: white;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;"); 

            break;
        case 3: // Radial Gap, D0
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter  \n outer(in)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Radial Gap\n  (in)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: white;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 4: // Radial Gap, Di
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter inner\n    (in)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Radial Gap (in)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: white;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 5: // Radial Gap, Davg
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter Mean\n    (in)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Radial Gap (in)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: white;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 6: // Annulus 
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Diameter Outter\n    (in)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Diameter Inner (in)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: white;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;

        case 7: // Rectangle
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Width\n    (inches)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Length\n  (inches)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: white;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;
        case 8: // Square
            showarea();
            ui.comboBox_2->hide();
            ui.label_2->setText("Side\n    (inches)");
            ui.lineEdit->show();
            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            ui.lineEdit_2->show();
            ui.lineEdit_2->setStyleSheet("background-color: grey;");
            ui.label_4->setText("Quantity");
            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");
            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");
            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");
            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");
            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            break;


        case 9:  //Round slot C-C 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText("Width (inches)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Length\n  (inches)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: white;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;

        case 10:  //Round slot E-E

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText("Width (inches)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Length\n  (inches)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: white;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText("0.444");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText("0.444");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText("1.39487");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText("0.15483");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText("0.15483");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;


        case 11:  //Ellipse 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText("Major Diameter  (in)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Minor Diameter\n  (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: white;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;


        case 12: //Semi Circle 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Diameter  (inches)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Radius \n  (inches)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");
            


            


          

           

            break;

            


        case 13: //Circular Sector 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Diameter  (inches)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Angle \n  (degrees)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: white;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;




         


        case 14:  //Right triangle 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Base  (inches)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Height (inches)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: white;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;



        case 15:  //Isosceles triangle 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Base  (inches)");
            //ui.lineEdit->setText(" ");


            ui.comboBox_3->hide();
            ui.label_3->setText("Height (inches)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: white;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;



        case 16:  //Dh, Peerimeter 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: white;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: white;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: grey;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;

        case 17:  //Dh, Area 

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: white;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: white;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;
        case 18:  // Peerimeter  Area

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: white;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color: white;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;

        case 19:  // Perimeter, DE

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: white;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: white;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color:grey ;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;

        case 20:  // Geometric, Area

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color:white ;");

            ui.label_9->setText("Total Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;

        case 21:  // Effective, Area

            showarea();


            ui.comboBox_2->hide();
            ui.label_2->setText(" Equivalent \n Gap(in)");
            //ui.lineEdit->setText(" ");
            ui.lineEdit->setStyleSheet("background-color: grey;");



            ui.comboBox_3->hide();
            ui.label_3->setText("Equivalent \n Radius (in)");
            //ui.lineEdit_2->hide();
            //ui.lineEdit_2->setText(" ");
            ui.lineEdit_2->setStyleSheet("background-color: grey;");




            ui.label_4->setText("Quantity");

            ui.label_5->setText("Equivalent \n Diameter\n   (in)");
            ui.lineEdit_3->setText(" ");
            ui.lineEdit_3->setStyleSheet("background-color: grey;");

            ui.label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui.lineEdit_4->setText(" ");
            ui.lineEdit_4->setStyleSheet("background-color: grey;");

            ui.lineEdit_5->setText(" ");
            ui.label_7->setText("Perimeter\nWetted(in)");
            ui.lineEdit_5->setStyleSheet("background-color: grey;");

            ui.label_8->setText("Effective \n Area(in-in)");
            ui.lineEdit_6->setText(" ");
            ui.lineEdit_6->setStyleSheet("background-color:white ;");

            ui.label_9->setText(" Total \n Effective \n Area\n  (in-in)");
            ui.lineEdit_7->setText(" ");
            ui.lineEdit_7->setStyleSheet("background-color: grey;");

            break;

            
      
            
        }
    }
}
