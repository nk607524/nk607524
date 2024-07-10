#include "bnr.h"
#include "ui_bnr.h"

Bnr::Bnr(QWidget *parent) :
    QWidget(parent),
    ui(new Ui::Bnr)
{
    ui->setupUi(this);


    connect(ui->comboBox, SIGNAL(activated(int)), this, SLOT(bydefultfun()));


}

Bnr::~Bnr()
{
    delete ui;
}

void Bnr::setMode(Bnr::Mode mode)
{
    currentmode = mode;

    if(mode == Fre)
    {
        ui->comboBox->addItem("bnr1");
        ui->comboBox->addItem("bnr2");
        ui->comboBox->addItem("bnr3");
        ui->comboBox->addItem("bnr4");
        ui->comboBox->addItem("bnr5");
        ui->comboBox->addItem("bnr6");
        ui->comboBox->addItem("bnr8");

    }
    else if(mode == Meter)
    {
        ui->comboBox->addItem("naveen1");
        ui->comboBox->addItem("naveen2");
        ui->comboBox->addItem("naveen3");
        ui->comboBox->addItem("naveen4");
        ui->comboBox->addItem("naveen5");
        ui->comboBox->addItem("naveen6");
        ui->comboBox->addItem("naveen7");

    }
    bydefultfun();

}

void Bnr::mapkrishna()
{
    int Ind = ui->comboBox->currentIndex();
    map1.clear();

        if (currentmode == Fre)
        {
            switch (Ind)
            {
            case 0:
                map1.insert("label1", "Narayana");
                map1.insert("label2", "Naveen");
                map1.insert("label3", "Moulali");
                map1.insert("label4", "Madhu");

                break;
            case 1:
                map1.insert("label1", "Narayana1");
                map1.insert("label2", "Naveen1");
                map1.insert("label3", "Moulali1");
                map1.insert("label4", "Madhu1");

                break;
            case 2:
                map1.insert("label1", "Narayana2");
                map1.insert("label2", "Naveen2");
                map1.insert("label3", "Moulali2");
                map1.insert("label4", "Madhu2");

                break;
            case 3:
                map1.insert("label1", "Narayana3");
                map1.insert("label2", "Naveen3");
                map1.insert("label3", "Moulali3");
                map1.insert("label4", "Madhu3");

                break;
            }

        }
        else if (currentmode == Meter)
        {
            switch (Ind)
            {
            case 0:
                map1.insert("label1", "Narayana");
                map1.insert("label2", "Naveen");
                map1.insert("label3", "Moulali");
                map1.insert("label4", "Madhu");

                break;
            case 1:
                map1.insert("label1", "Narayana1");
                map1.insert("label2", "Naveen1");
                map1.insert("label3", "Moulali1");
                map1.insert("label4", "Madhu1");

                break;
            case 2:
                map1.insert("label1", "Narayana2");
                map1.insert("label2", "Naveen2");
                map1.insert("label3", "Moulali2");
                map1.insert("label4", "Madhu2");

                break;
            case 3:
                map1.insert("label1", "Narayana3");
                map1.insert("label2", "Naveen3");
                map1.insert("label3", "Moulali3");
                map1.insert("label4", "Madhu3");

                break;
            }

        }
     qDebug()<<"mappppppppppp1"<<map1<<endl;

}

void Bnr::bydefultfun()
{
    mapkrishna();
    int Ind = ui->comboBox->currentIndex();
        if (currentmode == Fre)
        {
            ui->label->setText(map1.value("label1"));
            ui->label_2->setText(map1.value("label2"));
            ui->label_3->setText(map1.value("label3"));
            ui->label_4->setText(map1.value("label4"));


//            switch (Ind)
//            {
//            case 0:
//                ui->label->setText("bnr1");
//                break;
//            case 1:
//                ui->label->setText("bnr2");

//                break;
//            case 2:
//                ui->label->setText("bnr3");
//                break;
//            case 3:
//                ui->label->setText("bnr4");
//                break;
//            case 4:
//                ui->label->setText("bnr5");
//                break;
//            case 5:
//                ui->label->setText("bnr6");
//                break;
//            case 6:
//                ui->label->setText("bnr7");
//                break;
//            case 7:
//                ui->label->setText("bnr8");
//                break;
 //           }
        }
        else if (currentmode == Meter)
        {
            ui->label->setText(map1.value("label1"));
            ui->label_2->setText(map1.value("label2"));
            ui->label_3->setText(map1.value("label3"));
            ui->label_4->setText(map1.value("label4"));
//            switch (Ind)
//            {
//            case 0:
//                ui->label->setText("bnr1");
//                break;
//            case 1:
//                ui->label->setText("bnr2");

//                break;
//            case 2:
//                ui->label->setText("bnr3");
//                break;
//            case 3:
//                ui->label->setText("bnr4");
//                break;
//            case 4:
//                ui->label->setText("bnr5");
//                break;
//            case 5:
//                ui->label->setText("bnr6");
//                break;
//            case 6:
//                ui->label->setText("bnr7");
//                break;
//            case 7:
//                ui->label->setText("bnr8");
//                break;
//            }
        }
}
