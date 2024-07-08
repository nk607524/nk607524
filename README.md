#pragma once

#include <QWidget>
#include "ui_HeadLoss.h"
#include "HeadLoss.h"



class HeadLoss : public QWidget
{
	Q_OBJECT

public:
	HeadLoss(QWidget *parent = nullptr);
	~HeadLoss();


private slots:
	void handleComboBoxChange();


private:
	Ui::HeadLossClass ui;

	void showCraneFlow();
	void showUserInput();

};




#include "HeadLoss.h"

HeadLoss::HeadLoss(QWidget *parent)
	: QWidget(parent)
{
	ui.setupUi(this);

	ui.comboBox->addItem("Crane Flow Of Fluids");
	ui.comboBox->addItem("User Input");

	connect(ui.comboBox, SIGNAL(activated(int)), this, SLOT(handleComboBoxChange()));

}

HeadLoss::~HeadLoss()
{}

void HeadLoss::handleComboBoxChange()
{
    int index = ui.comboBox->currentIndex();
    if (index == 0) // Crane Flow
    {
        showCraneFlow();
    }
    else if (index == 1) // User Input
    {
        showUserInput();
    }
}


void HeadLoss::showCraneFlow()
{
    ui.label_2->show();
    ui.lineEdit->show();

    ui.label_3->hide();
    ui.lineEdit_2->hide();
}

void HeadLoss::showUserInput()
{
    ui.label_2->show();
    ui.lineEdit->show();

    ui.label_3->show();
    ui.lineEdit_2->show();
}
