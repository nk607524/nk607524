#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include <QWidget>
#include <QStringList>
#include <QDebug>
#include <QComboBox>
#include "Util.h"

QT_BEGIN_NAMESPACE
namespace Ui { class MainWindow; }
QT_END_NAMESPACE

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    MainWindow(QWidget *parent = nullptr);
    ~MainWindow();
    struct FlowTypeLabel
       {
           en_FlowSectionType L_flowAreaType;
           QString l_strLabel1;
           QString l_strLabel2;
           QString l_strLabel3;
           QString l_strLabel4;
           QString l_strLabel5;
           QString l_strLabel6;
           QString l_strLabel7;
           QString l_strLabel8;
           bool l_bCombo1Enabled;
           bool l_bCombo2Enabled;
           bool l_bEdit1Enabled;
           bool l_bEdit2Enabled;

           en_FlowSectionType getType() const { return L_flowAreaType; }
           void setType(en_FlowSectionType newType) { L_flowAreaType = newType; }

           QString getLabel1Text() const { return l_strLabel1; }
           QString getLabel2Text() const { return l_strLabel2; }
           QString getLabel3Text() const { return l_strLabel3; }
           void setLabel1Text(const QString& text) { l_strLabel1 = text; }
           void setLabel2Text(const QString& text) { l_strLabel2 = text; }
           void setLabel3Text(const QString& text) { l_strLabel3 = text; }
           bool isCombo1Enabled() const { return l_bCombo1Enabled; }
           bool isCombo2Enabled() const { return l_bCombo2Enabled; }
           bool isEdit1Enabled() const { return l_bEdit1Enabled; }
           bool isEdit2Enabled() const { return l_bEdit2Enabled; }
           void setEdit1Enabled(bool enabled) { l_bEdit1Enabled = enabled; }
           void setEdit2Enabled(bool enabled) { l_bEdit2Enabled = enabled; }
       };

       FlowTypeLabel flowArea;
       QStringList hideshow;
private slots:
    void onComboBoxChanged(int index);

private:
    Ui::MainWindow *ui;
    QStringList getEnumStringList() const;
    en_FlowSectionType indexToEnum(int index) const;
    void updateUI(en_FlowSectionType type);
    FlowTypeLabel getLabels(en_FlowSectionType type);

};
#endif // MAINWINDOW_H



#include "mainwindow.h"
#include "ui_mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);

//    QMetaEnum metaEnum = QMetaEnum::fromType<flowArea.L_flowAreaType>();
//        for (int i = 0; i < metaEnum.keyCount(); ++i) {
//            ui->comboBox->addItem(metaEnum.key(i), metaEnum.value(i));
//        }
//    for (int i = 0; i < voltageRangeEnum.keyCount(); ++i) {
//        qDebug()<<"bnrr2345678"<<voltageRangeEnum.key(i), voltageRangeEnum.value(i);
//        ui->comboBox->addItem(voltageRangeEnum.key(i), voltageRangeEnum.value(i));
//    }


    ui->comboBox->addItems(getEnumStringList());
       connect(ui->comboBox, QOverload<int>::of(&QComboBox::currentIndexChanged), this, &MainWindow::onComboBoxChanged);

       flowArea.setType(STANDARD_DRILL);
       updateUI(flowArea.getType());
}

MainWindow::~MainWindow()
{
    delete ui;
}
QStringList MainWindow::getEnumStringList() const
{
    return {
        "Standard Drill", "Circle", "Axial Gap", "Radial Gap, Do", "Radial Gap, Di",
        "Radial Gap, Davg", "Annulus", "Rectangle", "Square", "Round End Slot",
        "Round Slot, C-C", "Round Slot, E-E", "Ellipse", "Semi Circle", "Circular Sector",
        "Right Triangle", "Isosceles Triangle", "Dh, Perimeter", "Dh, Area",
        "Perimeter, Area", "Perimeter, De", "Standard Tube", "Non-Standard Tube",
        "Circular, Do, Tw", "Circular, Di", "Geometric Area", "Effective Area"
    };
}

en_FlowSectionType MainWindow::indexToEnum(int index) const
{
    switch (index) {
    case 0: return STANDARD_DRILL;
    case 1: return CIRCLE;
    case 2: return AXIAL_GAP;
    case 3: return RADIAL_GAP_DO;
    case 4: return RADIAL_GAP_DI;
    case 5: return RADIAL_GAP_DAVG;
    case 6: return ANNULUS;
    case 7: return RECTANGLE;
    case 8: return SQUARE;
    case 9: return ROUND_END_SLOT;
    case 10: return ROUND_SLOT_CC;
    case 11: return ROUND_SLOT_EE;
    case 12: return ELLIPSE;
    case 13: return SEMI_CIRCLE;
    case 14: return CIRCULAR_SECTOR;
    case 15: return RIGHT_TRIANGLE;
    case 16: return ISOSCELES_TRIANGLE;
    case 17: return DH_PERIMETER;
    case 18: return DH_AREA;
    case 19: return PERIMETER_AREA;
    case 20: return PERIMETER_DE;
    case 21: return STANDARD_TUBE;
    case 22: return NONSTANDARD_TUBE;
    case 23: return CIRCULAR_DO_TW;
    case 24: return CIRCULAR_DI;
    case 25: return GEOMETRIC_AREA;
    case 26: return EFFECTIVE_AREA;
    default: return STANDARD_DRILL;
    }
}

void MainWindow::onComboBoxChanged(int index)
{
    flowArea.setType(indexToEnum(index));
    updateUI(flowArea.getType());
    qDebug() << "Selected Flow Area Type:" << index;
}

void MainWindow::updateUI(en_FlowSectionType type)
{
    FlowTypeLabel labels = getLabels(type);

    ui->label_2->setText(labels.getLabel1Text());
    ui->label_3->setText(labels.getLabel2Text());
    ui->label_4->setText(labels.getLabel3Text());

    ui->comboBox_2->setEnabled(labels.isCombo1Enabled());
    ui->comboBox_3->setEnabled(labels.isCombo2Enabled());

    ui->lineEdit_2->setEnabled(labels.isEdit1Enabled());
    ui->lineEdit_3->setEnabled(labels.isEdit2Enabled());

    // Apply specific hiding logic here if necessary
}

MainWindow::FlowTypeLabel MainWindow::getLabels(en_FlowSectionType type)
{
    FlowTypeLabel label;
    label.setType(type);

    switch (type) {
    case STANDARD_DRILL:
        label.setLabel1Text("Diameter Inches(in)");
        label.setLabel2Text("bnr Inner12345(in)");
        label.setEdit1Enabled(false);
        label.setEdit2Enabled(false);
        break;
    case CIRCLE:
        label.setLabel1Text("circle Inches(in)");
        label.setLabel2Text("crile2");
        label.setEdit1Enabled(true);
        label.setEdit2Enabled(true);
        break;
    // Add cases for other enum values and initialize the labels and enabled states accordingly
    default:
        break;
    }

    return label;
}



