#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include "form.h"
#include "ui_form.h"

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

private slots:
    void on_toolBox_2_currentChanged(int index);

private:
    Ui::MainWindow *ui;
};
#endif // MAINWINDOW_H
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

    Ui::Form *ui;

private:

};

#endif // FORM_H
#include "mainwindow.h"
#include "ui_mainwindow.h"
#include <QDebug>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);
    connect(ui->comboBox,SIGNAL(activated(int)),this,SLOT(naveen()));

}

MainWindow::~MainWindow()
{
    delete ui;
}




void MainWindow::naveen()
{
    bnr = ui->comboBox->currentIndex();


    qDebug()<<"bnr start222"<<bnr<<endl;

    Form *naveen11234 = new Form();
    if(bnr == 0)
    {
                QPixmap pixmap("/home/linkwell/toolbox/lakshadweep.png");
   naveen11234->ui->label->setPixmap(pixmap);
    }
    else if(bnr == 1)
    {
          QPixmap pixmap("/home/linkwell/toolbox/ManipurGovtLogoOLD.png");
        naveen11234->ui->label->setPixmap(pixmap);
    }
    else if(bnr == 2)
    {
          QPixmap pixmap("/home/linkwell/toolbox/NagalandGovtLogo_ORG.png");
        naveen11234->ui->label->setPixmap(pixmap);
    }


   naveen11234->show();



}
#include "form.h"
#include "ui_form.h"
#include <QDebug>

Form::Form(QWidget *parent) :
    QWidget(parent),
    ui(new Ui::Form)
{
   ui->setupUi(this);

       ui->label->setAutoFillBackground(true);


}
Form::~Form() {
    delete ui;  // Clean up the Ui pointer
}

