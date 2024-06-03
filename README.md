#include "mainwindow.h"
#include "ui_mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);
    connect(ui->actionAbout, &QAction::triggered, this, &MainWindow::showmsg);

}

MainWindow::~MainWindow()
{
    delete ui;
}

void MainWindow::showmsg()
{
   
    QMessageBox msgBox;
    msgBox.setWindowTitle("Message with Image");
    QLabel *imageLabel = new QLabel(&msgBox);

    QPixmap pixmap(":/image/iris.png"); // Ensure the path to your image is correct
    imageLabel->setPixmap(pixmap);
    imageLabel->setGeometry(10,30,50,50);
    msgBox.setText("Visual Network Version 9.2.0.0 \n"
                   "Copyright @ Honeywell International Inc.,2006-2021.All rights reseved \n"
                   "This software, all information and expression contains trade secrets and \n"
                   "May  ");



          QVBoxLayout *layout = new QVBoxLayout;
          layout->addWidget(imageLabel);

          msgBox.layout()->addItem(layout);


    msgBox.exec();

}


#include "mainwindow.h"
#include "ui_mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);
    connect(ui->actionAbout, &QAction::triggered, this, &MainWindow::showmsg);


}

MainWindow::~MainWindow()
{
    delete ui;
}

void MainWindow::showmsg()
{
   
    QMessageBox msgBox;
    msgBox.setWindowTitle("Message with Image");
    QLabel *imageLabel = new QLabel(&msgBox);

    QPixmap pixmap(":/image/iris.png"); // Ensure the path to your image is correct
    imageLabel->setPixmap(pixmap);
    imageLabel->setGeometry(10,30,50,50);
    msgBox.setText("Visual Network Version 9.2.0.0 \n"
                   "Copyright @ Honeywell International Inc.,2006-2021.All rights reseved \n"
                   "This software, all information and expression contains trade secrets and \n"
                   "May  ");



          QVBoxLayout *layout = new QVBoxLayout;
          layout->addWidget(imageLabel);

          msgBox.layout()->addItem(layout);


    msgBox.exec();


}


