#ifndef FORM_H
#define FORM_H

#include <QWidget>
#include "mainwindow.h"

namespace Ui {
class Form;
}

class Form : public QWidget
{
    Q_OBJECT

public:
    explicit Form(QWidget *parent = nullptr);
    ~Form();
    int bnr;

    Ui::Form *ui;

public slots:
    void showtime();
    void naveen();


private:

};

#endif // FORM_H


#include "form.h"
#include "ui_form.h"
#include <QDebug>

Form::Form(QWidget *parent) :
    QWidget(parent),
    ui(new Ui::Form)
{
    ui->setupUi(this);
    ui->comboBox->addItem("ingress");
    ui->comboBox->addItem("Egress");

    ui->comboBox->addItem("used input");

    ui->comboBox->addItem("Huning");


    ui->comboBox->addItem("Parker & Kercher");

    ui->comboBox->addItem("Binder");


    naveen();
    connect(ui->comboBox,SIGNAL(activated(int)),this,SLOT(naveen()));



}
Form::~Form() {
    delete ui;  // Clean up the Ui pointer
}
void Form::showtime()
{
    ui->label_1->show();
    ui->label_2->show();
    ui->lineEdit_1->show();
    ui->label_3->show();
    ui->label_4->show();
    ui->lineEdit_2->show();
    ui->lineEdit_3->show();
    ui->lineEdit_4->show();
    ui->label->show();
    ui->comboBox_2->show();
}
void Form::naveen()
{
    bnr = ui->comboBox->currentIndex();


    qDebug()<<"bnr start222"<<bnr<<endl;
    if(bnr == 0)
    {
        showtime();

        QPixmap pixmap("/home/linkwell/live_project/lakshadweep.png");
        ui->label_4->setPixmap(pixmap);
        ui->label_1->setText("Tuning \n Factor");
        ui->lineEdit_1->setText("1.0");
        ui->comboBox_2->addItem("open with no overlap K=1");
        ui->label_2->hide();
        ui->label_3->hide();
        ui->lineEdit_4->hide();
        ui->lineEdit_2->hide();
        ui->lineEdit_3->hide();


    }
    else if(bnr == 1)
    {
        showtime();

        QPixmap pixmap("/home/linkwell/live_project/ManipurGovtLogoOLD.png");
        ui->label_4->setPixmap(pixmap);
        ui->label_1->setText("Tuning \n Factor");
        ui->lineEdit_1->setText("1.0");
        ui->comboBox_2->addItem("open with no overlap K=1");

        ui->label_2->hide();
        ui->label_3->hide();
        ui->lineEdit_4->hide();
        ui->lineEdit_2->hide();
        ui->lineEdit_3->hide();
    }
    else if(bnr == 2)
    {
        showtime();

        // QPixmap pixmap("/home/linkwell/toolbox/NagalandGovtLogo_ORG.png");
        ui->label_1->hide();
        ui->label_2->hide();
        ui->lineEdit_1->hide();
        ui->label_3->hide();
        ui->label_4->hide();
        ui->lineEdit_4->setText("0.7");
        ui->lineEdit_3->hide();
        ui->lineEdit_2->hide();

        ui->label->hide();
        ui->comboBox_2->hide();
    }
    else if(bnr == 3)
    {
        showtime();

        QPixmap pixmap("/home/linkwell/live_project/NagalandGovtLogo_ORG.png");
        ui->label_4->setPixmap(pixmap);
        ui->label_1->setText("Orifice \n Length \n  (in)");
        ui->lineEdit_1->setText("0.1000");
        ui->label_2->setText("Orifice \nFillet Radius \n   (in)");
        ui->lineEdit_2->setText("0.01");
        ui->label_3->setText("BETA");
        ui->lineEdit_4->hide();
        ui->lineEdit_3->setText("0.0");
        ui->label->hide();
        ui->comboBox_2->hide();
    }
    else if(bnr == 4)
    {
        showtime();

        QPixmap pixmap("/home/linkwell/live_project/mark.png");
        ui->label_4->setPixmap(pixmap);
        ui->label_1->setText("Orifice \n Length \n  (in)");
        ui->lineEdit_1->setText("0.1000");
        ui->label_2->setText("Orifice \nFillet Radius \n   (in)");
        ui->lineEdit_2->setText("0.01");
        ui->label_3->setText("BETA");
        ui->lineEdit_4->hide();
        ui->lineEdit_3->setText("0.0");
        ui->label->hide();
        ui->comboBox_2->hide();
    }
    else if(bnr == 5)
    {
        showtime();
        QPixmap pixmap("/home/linkwell/live_project/mark.png");

        ui->label_4->setPixmap(pixmap);
        ui->label_1->setText("Orifice \n Length \n  (in)");
        ui->lineEdit_1->setText("0.1000");
        ui->label_2->setText("Orifice \nFillet Radius \n   (in)");
        ui->lineEdit_2->setText("0.01");
        ui->label_3->setText("BETA");
        ui->lineEdit_4->hide();
        ui->lineEdit_3->setText("0.0");
        ui->label->hide();
        ui->comboBox_2->hide();
    }

}



