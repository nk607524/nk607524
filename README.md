#pragma once

#include <QtWidgets/QMainWindow>
#include "ui_Aboutvn.h"
#include "QtWidgetsClass.h"

//#include "QtWidgetsClass.h"

class Aboutvn : public QMainWindow
{
    Q_OBJECT

public:
    Aboutvn(QWidget *parent = nullptr);
    ~Aboutvn();
public slots:
    void showHelpWidget();
    
private:
    Ui::AboutvnClass ui;
};

#include "Aboutvn.h"

Aboutvn::Aboutvn(QWidget *parent)
    : QMainWindow(parent)
{
    ui.setupUi(this);
    connect(ui.actionAbout, &QAction::triggered, this, &Aboutvn::showHelpWidget);
     Naveen = "Visusal Network version 9.2.0.0 \n copy right Honeywell International inc > , 2006 - 2021.All rights reserved/n This software, all informationand expression contains trade secretsand/nmay not, in whole or in part, be licenced, used, duplicate, or disclosed for any purpose without prior written permission of Honeywell/ninternational inc/n";

}

Aboutvn::~Aboutvn()
{}

void Aboutvn::showHelpWidget()
{
    QtWidgetsClass *widget = new QtWidgetsClass(this);
    widget->show(); 
}


#pragma once

#include <QMainWindow>
#include "ui_QtWidgetsClass.h"

class QtWidgetsClass : public QMainWindow
{
	Q_OBJECT

public:
	QtWidgetsClass(QWidget *parent = nullptr);
	~QtWidgetsClass();
private slots:
	void on_okButton_clicked();

private:
	Ui::QtWidgetsClassClass ui;
};

#include "Aboutvn.h"

Aboutvn::Aboutvn(QWidget *parent)
    : QMainWindow(parent)
{
    ui.setupUi(this);
    connect(ui.actionAbout, &QAction::triggered, this, &Aboutvn::showHelpWidget);
}

Aboutvn::~Aboutvn()
{}

void Aboutvn::showHelpWidget()
{
    QtWidgetsClass *widget = new QtWidgetsClass(this);
    widget->show(); 
}
