#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include "form.h"
#include "ui_form.h"
#include <QDebug>

QT_BEGIN_NAMESPACE
namespace Ui { class MainWindow; }
QT_END_NAMESPACE

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    MainWindow(QWidget *parent = nullptr);
    ~MainWindow();
    int bnr;


public slots:
    void naveen();
    void showtime();


private slots:
private:
    Ui::MainWindow *ui;
};
#endif // MAINWINDOW_H

#include "mainwindow.h"
#include "mainwindow.h"
#include "ui_mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);
    naveen();
    connect(ui->comboBox_4,SIGNAL(activated(int)),this,SLOT(naveen()));
}

MainWindow::~MainWindow()
{
    delete ui;
}
void MainWindow::naveen()
{
    bnr = ui->comboBox_4->currentIndex();


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

void MainWindow::showtime()
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

