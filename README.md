
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
    ui->label_23->show();
    ui->label_20->show();
    ui->lineEdit_8->show();
    ui->label_25->show();
    ui->label_24->show();
    ui->lineEdit_9->show();
    ui->lineEdit_10->show();
    ui->lineEdit_11->show();
}
void Form::naveen()
{
    bnr = ui->comboBox->currentIndex();


    qDebug()<<"bnr start222"<<bnr<<endl;
    if(bnr == 0)
    {
        showtime();

                QPixmap pixmap("/home/linkwell/live_project/lakshadweep.png");
                ui->label_23->setPixmap(pixmap);
                ui->label_20->setText("Tuning \n Factor");
                ui->lineEdit_8->setText("1.0");
                ui->label_25->hide();
                ui->label_24->hide();
                ui->lineEdit_9->hide();
                ui->lineEdit_10->hide();
                ui->lineEdit_11->hide();

    }
    else if(bnr == 1)
    {
        showtime();

          QPixmap pixmap("/home/linkwell/live_project/ManipurGovtLogoOLD.png");
          ui->label_23->setPixmap(pixmap);
          ui->label_20->setText("Tuning \n Factor");
          ui->lineEdit_8->setText("1.0");
          ui->label_25->hide();
          ui->label_24->hide();
          ui->lineEdit_9->hide();
          ui->lineEdit_10->hide();
          ui->lineEdit_11->hide();
    }
    else if(bnr == 2)
    {
        showtime();

         // QPixmap pixmap("/home/linkwell/toolbox/NagalandGovtLogo_ORG.png");
          ui->label_23->hide();
          ui->label_20->hide();
          ui->lineEdit_8->hide();
          ui->label_25->hide();
          ui->label_24->hide();
          ui->lineEdit_9->setText("0.7");
          ui->lineEdit_10->hide();
          ui->lineEdit_11->hide();
    }
    else if(bnr == 3)
     {
        showtime();

        QPixmap pixmap("/home/linkwell/live_project/NagalandGovtLogo_ORG.png");
        ui->label_23->setPixmap(pixmap);
        ui->label_20->setText("Orifice \n Length \n  (in)");
        ui->lineEdit_8->setText("0.1000");
        ui->label_25->setText("Orifice \nFillet Radius \n   (in)");
        ui->lineEdit_10->setText("0.01");
        ui->label_24->setText("BETA");
        ui->lineEdit_9->hide();
        ui->lineEdit_11->setText("0.0");
    }
    else if(bnr == 4)
     {
        showtime();

        QPixmap pixmap("/home/linkwell/live_project/mark.png");
        ui->label_23->setPixmap(pixmap);
        ui->label_20->setText("Orifice \n Length \n  (in)");
        ui->lineEdit_8->setText("0.1000");
        ui->label_25->setText("Orifice \nFillet Radius \n   (in)");
        ui->lineEdit_10->setText("0.01");
        ui->label_24->setText("BETA");
        ui->lineEdit_9->hide();
        ui->lineEdit_11->setText("0.0");
    }
    else if(bnr == 5)
    {
        showtime();

          ui->label_23->hide();
          ui->label_20->hide();
          ui->lineEdit_8->hide();
          ui->label_25->hide();
          ui->label_24->hide();
          ui->lineEdit_9->hide();
          ui->lineEdit_10->hide();
          ui->lineEdit_11->hide();
    }
}


