#ifndef FLOWAREA_H
#define FLOWAREA_H

#include <QWidget>
#include "mainwindow.h"
#include "ui_mainwindow.h"

namespace Ui {
class FlowArea;
}

class FlowArea : public QWidget
{
    Q_OBJECT

public:
    explicit FlowArea(QWidget *parent = nullptr);
    ~FlowArea();
    int bnr;
    Ui::FlowArea *ui;
    void showarea();
public slots:
void flowareadisplay();

private:
};

#endif // FLOWAREA_H


#include "flowarea.h"
#include "ui_flowarea.h"

FlowArea::FlowArea(QWidget *parent) :
    QWidget(parent),
    ui(new Ui::FlowArea)
{
    ui->setupUi(this);
    changebnr = new Sample();
    qDebug()<<"output of file"<<changebnr->krishnabnr<<endl;
    if(changebnr->krishnabnr =="bnr1")
    {
        ui->comboBox->addItem("Standard Tube");

        ui->comboBox->addItem("Non-Standard Tube");
        ui->comboBox->addItem("Dh,Perimeter");

        ui->comboBox->addItem("Dh,Area");
        flowareadisplay();
    }
    else if(changebnr->krishnabnr =="bnr2")
    {
        ui->comboBox->addItem("Standard Drill Size");

        ui->comboBox->addItem("Circular");

        flowareadisplay();
    }
    connect(ui->comboBox,SIGNAL(activated(int)),this,SLOT(flowareadisplay()));

}

FlowArea::~FlowArea()
{
    delete ui;
}

void FlowArea::showarea()
{
    ui->comboBox_2->show();
    ui->comboBox_3->show();
    ui->lineEdit_2->show();
    ui->lineEdit_3->show();

}

void FlowArea::flowareadisplay()
{
    if(changebnr->krishnabnr == "bnr1")
    {
        bnr = ui->comboBox->currentIndex();
        if(bnr == 0) // Standard Tube
        {
            showarea();
            ui->comboBox_2->addItem("0.5000");
            ui->label_2->setText("Diameter Outer\n    (in)");
            ui->lineEdit_2->hide();
            ui->label_3->setText("Thickness Wall\n  (in)");
            ui->lineEdit_3->setStyleSheet("background-color: grey;");

            ui->lineEdit_3->setText("0.028");
            ui->label_4->setText("Quantity");
            ui->label_5->setText("Equivalent \n Diameter\n   (in)");
            ui->lineEdit_5->setText("0.444");
            ui->lineEdit_5->setStyleSheet("background-color: grey;");

            ui->label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui->lineEdit_6->setText("0.444");
            ui->lineEdit_6->setStyleSheet("background-color: grey;");

            ui->lineEdit_7->setText("1.39487");
            ui->label_7->setText("Perimeter\nWetted(in)");
            ui->lineEdit_7->setStyleSheet("background-color: grey;");

            ui->label_8->setText("Area(in-in)");
            ui->lineEdit_8->setText("0.15483");
            ui->lineEdit_8->setStyleSheet("background-color: grey;");

            ui->label_9->setText("Total Area\n  (in-in)");
            ui->lineEdit_9->setText("0.15483");
            ui->lineEdit_9->setStyleSheet("background-color: grey;");

        }
        else if(bnr == 1) // Non-Standard Tube
        {
            showarea();

            ui->comboBox_2->addItem("0.5000");
            ui->label_2->setText("Diameter Outer\n    (in)");
            ui->lineEdit_2->hide();
            ui->label_3->setText("Thickness Wall\n  (in)");
            ui->lineEdit_3->hide();
            ui->comboBox_3->addItem("0.035");
            ui->label_4->setText("Quantity");
            ui->label_5->setText("Equivalent \n Diameter\n   (in)");
            ui->lineEdit_5->setText("0.444");
            ui->label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui->lineEdit_6->setText("0.444");
            ui->lineEdit_7->setText("1.39487");
            ui->label_7->setText("Perimeter\nWetted(in)");
            ui->label_8->setText("Area(in-in)");
            ui->lineEdit_8->setText("0.15483");
            ui->label_9->setText("Total Area\n  (in-in)");
            ui->lineEdit_9->setText("0.15483");
            ui->lineEdit_5->setStyleSheet("background-color: grey;");
            ui->lineEdit_6->setStyleSheet("background-color: grey;");
            ui->lineEdit_7->setStyleSheet("background-color: grey;");
            ui->lineEdit_8->setStyleSheet("background-color: grey;");
            ui->lineEdit_9->setStyleSheet("background-color: grey;");



        }
        else if(bnr == 2) //Dh perimeter
        {
            showarea();

            ui->label_2->setText("Equivalent cric\n Gap(in)");
            ui->lineEdit_2->setText("");
            ui->comboBox_2->hide();
            ui->label_3->setText("Equivalent \nRadius(in)");
            ui->lineEdit_3->setText("");
            ui->comboBox_3->hide();
            ui->label_4->setText("Quantity");
            ui->label_5->setText("Equivalent \n Diameter\n   (in)");
            ui->lineEdit_5->setText("");
            ui->label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui->lineEdit_6->setText("");
            ui->lineEdit_7->setText("");
            ui->label_7->setText("Perimeter\nWetted(in)");
            ui->label_8->setText("Area(in-in)");
            ui->lineEdit_8->setText("");
            ui->label_9->setText("Total Area\n  (in-in)");
            ui->lineEdit_9->setText("");
            ui->lineEdit_5->setStyleSheet("background-color: grey;");
            ui->lineEdit_6->setStyleSheet("background-color: grey;");
            ui->lineEdit_7->setStyleSheet("background-color: white;");
            ui->lineEdit_8->setStyleSheet("background-color: white;");
            ui->lineEdit_9->setStyleSheet("background-color: grey;");
            ui->lineEdit_2->setStyleSheet("background-color: grey;");
            ui->lineEdit_3->setStyleSheet("background-color: grey;");

        }
        else if(bnr == 3) //Dh Area
        {
            showarea();

            ui->label_2->setText("Equivalent cric\n Gap(in)");
            ui->lineEdit_2->setText("");
            ui->comboBox_2->hide();
            ui->label_3->setText("Equivalent \nRadius(in)");
            ui->lineEdit_3->setText("");
            ui->comboBox_3->hide();
            ui->label_4->setText("Quantity");
            ui->label_5->setText("Equivalent \n Diameter\n   (in)");
            ui->lineEdit_5->setText("");
            ui->label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui->lineEdit_6->setText("");
            ui->lineEdit_7->setText("");
            ui->label_7->setText("Perimeter\nWetted(in)");
            ui->label_8->setText("Area(in-in)");
            ui->lineEdit_8->setText("");
            ui->label_9->setText("Total Area\n  (in-in)");
            ui->lineEdit_9->setText("");
            ui->lineEdit_5->setStyleSheet("background-color: grey;");
            ui->lineEdit_6->setStyleSheet("background-color: white;");
            ui->lineEdit_7->setStyleSheet("background-color: grey;");
            ui->lineEdit_8->setStyleSheet("background-color: white;");
            ui->lineEdit_9->setStyleSheet("background-color: grey;");
            ui->lineEdit_2->setStyleSheet("background-color: grey;");
            ui->lineEdit_3->setStyleSheet("background-color: grey;");
        }
    }
    else if(changebnr->krishnabnr == "bnr2") //fre
    {
        bnr = ui->comboBox->currentIndex();
        if(bnr == 0) // Standard Tube
        {
            showarea();
            ui->comboBox_2->addItem("0.25");
            ui->label_2->setText("Diameter \ninchens(in)");
            ui->lineEdit_2->hide();
            ui->label_3->setText("Drill Set \n");
            ui->comboBox_3->addItem("Fractional");

            ui->lineEdit_3->hide();
            ui->label_4->setText("Quantity");
            ui->label_5->setText("Equivalent \n Diameter\n   (in)");
            ui->lineEdit_5->setText("0.444");
            ui->lineEdit_5->setStyleSheet("background-color: grey;");

            ui->label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui->lineEdit_6->setText("0.444");
            ui->lineEdit_6->setStyleSheet("background-color: grey;");

            ui->lineEdit_7->setText("1.39487");
            ui->label_7->setText("Perimeter\nWetted(in)");
            ui->lineEdit_7->setStyleSheet("background-color: grey;");

            ui->label_8->setText("Area(in-in)");
            ui->lineEdit_8->setText("0.15483");
            ui->lineEdit_8->setStyleSheet("background-color: grey;");

            ui->label_9->setText("Total Area\n  (in-in)");
            ui->lineEdit_9->setText("0.15483");
            ui->lineEdit_9->setStyleSheet("background-color: grey;");

        }
        else if(bnr == 1) //circular
        {
            showarea();

            ui->label_2->setText("Diameter\n(inches");
            ui->lineEdit_2->setText("");
            ui->comboBox_2->hide();
            ui->label_3->setText("Radius\n(inches)");
            ui->lineEdit_3->setText("");
            ui->comboBox_3->hide();
            ui->label_4->setText("Quantity");
            ui->label_5->setText("Equivalent \n Diameter\n   (in)");
            ui->lineEdit_5->setText("");
            ui->label_6->setText("Hydraulic\nDiameter\n  (in)");
            ui->lineEdit_6->setText("");
            ui->lineEdit_7->setText("");
            ui->label_7->setText("Perimeter\nWetted(in)");
            ui->label_8->setText("Area(in-in)");
            ui->lineEdit_8->setText("");
            ui->label_9->setText("Total Area\n  (in-in)");
            ui->lineEdit_9->setText("");
            ui->lineEdit_5->setStyleSheet("background-color: grey;");
            ui->lineEdit_6->setStyleSheet("background-color: grey;");
            ui->lineEdit_7->setStyleSheet("background-color: grey;");
            ui->lineEdit_8->setStyleSheet("background-color: grey;");
            ui->lineEdit_9->setStyleSheet("background-color: grey;");
            ui->lineEdit_2->setStyleSheet("background-color: white;");
            ui->lineEdit_3->setStyleSheet("background-color: grey;");
        }
    }

}

