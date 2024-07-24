#pragma once

#include <QWidget>
#include "ui_Flow_Area.h"
#include <QStringList>
#include <QDebug>
#include "Util.h"  

class Flow_Area : public QWidget
{
    Q_OBJECT

public:
    Flow_Area(QWidget* parent = nullptr);
    ~Flow_Area();

    // Struct with an enum inside
    struct FlowArea
    {
        en_FlowSectionType L_flowAreaType;

        // Getter for the enum type
        en_FlowSectionType getType() const {
            return L_flowAreaType;
        }

        // Setter for the enum type
        void setType(en_FlowSectionType newType) {
            L_flowAreaType = newType;
        }
    };

    FlowArea flowArea;
     void showall();
    QStringList hideshow;

private slots:
    void onComboBoxChanged(int index);

private:
    Ui::Flow_AreaClass ui;
    QStringList getEnumStringList() const;
    en_FlowSectionType indexToEnum(int index) const;
    void updateUI(en_FlowSectionType type);
};

















#include "Flow_Area.h"

// Constructor
Flow_Area::Flow_Area(QWidget* parent)
    : QWidget(parent)
{
    ui.setupUi(this);
    ui.comboBox->addItems(getEnumStringList());
    connect(ui.comboBox, QOverload<int>::of(&QComboBox::currentIndexChanged), this, &Flow_Area::onComboBoxChanged);

    // Initialize with the default value
    flowArea.setType(STANDARD_DRILL);
    updateUI(flowArea.getType());
}

// Destructor
Flow_Area::~Flow_Area()
{
}

// Populate the combo box with human-readable names
QStringList Flow_Area::getEnumStringList() const
{
    QStringList enumList;
    enumList << "Standard Drill" << "Circle" << "Axial Gap" << "Radial Gap, Do" << "Radial Gap, Di"
        << "Radial Gap, Davg" << "Annulus" << "Rectangle" << "Square" << "Round End Slot"
        << "Round Slot, C-C" << "Round Slot, E-E" << "Ellipse" << "Semi Circle" << "Circular Sector"
        << "Right Triangle" << "Isosceles Triangle" << "Dh, Perimeter" << "Dh, Area"
        << "Perimeter, Area" << "Perimeter, De" << "Standard Tube" << "Non-Standard Tube"
        << "Circular, Do, Tw" << "Circular, Di" << "Geometric Area" << "Effective Area";
    return enumList;
}

// Convert combo box index to enum
en_FlowSectionType Flow_Area::indexToEnum(int index) const
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
    case 15: return RIGHT_TRAINGLE;
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
    default: return STANDARD_DRILL; // Default case
    }
}

// Handle combo box selection change
void Flow_Area::onComboBoxChanged(int index)
{
    // Update the current flow area type based on the combo box selection
    flowArea.setType(indexToEnum(index));

    // Update the UI based on the selected type
    updateUI(flowArea.getType());
    

    // Log the current flow area type for debugging
    qDebug() << "Selected Flow Area Type:" << index;
}

// Update the UI based on the selected flow area type
void Flow_Area::updateUI(en_FlowSectionType type)
{
    QStringList listdata;
    listdata.clear();
    hideshow.clear();
    switch (type) {
    case CIRCLE:
        //ui.label_3->setText("Radius Inches");
       // ui.lineEdit_2->setDisabled(true);
 listdata <<"Normal Flow Section"<<"Diameter \n Inches(in)"<<"Dril Set"<<"Quantity"<<"Equivalent \n Daimeter(in)"<<"Hydraulic \n Diameter(in)"<<"Permeter \nWetted(in)"<<"Area(in-in)"<<"Total Area(in-in)";
        hideshow <<"6"<<"7"<<"8"<<"9"<<"com1"<<"com2";
        break;
    case STANDARD_DRILL:
       // ui.label->setText("Standard Drill Label");
        //ui.lineEdit->setEnabled(true);
        //ui.label_3->setText("Another Label for Standard Drill");
       // ui.lineEdit_2->setEnabled(true);
        listdata <<"Normal Flow Section"<<"Diameter \n Inches(in)"<<"Dril Set"<<"Quantity"<<"Equivalent \n Daimeter(in)"<<"Hydraulic \n Diameter(in)"<<"Permeter \nWetted(in)"<<"Area(in-in)"<<"Total Area(in-in)";
        hideshow <<"6"<<"7"<<"8"<<"9"<<"com1"<<"com2";
        break;
    case AXIAL_GAP:
       // ui.label_2->setText("Axial Gap Label");
       // ui.lineEdit_2->setEnabled(true);
        listdata <<"Normal Flow Section"<<"Diameter \n Inches(in)"<<"Dril Set"<<"Quantity"<<"Equivalent \n Daimeter(in)"<<"Hydraulic \n Diameter(in)"<<"Permeter \nWetted(in)"<<"Area(in-in)"<<"Total Area(in-in)";
        hideshow <<"6"<<"7"<<"8"<<"9"<<"com1"<<"com2";
        break;
        // Add other cases with their specific UI updates
   // default:
        // Reset to default state for all other types
        //ui.label->setText("Default Label 1");
      //  ui.label_2->setText("Default Label 2");
       // ui.label_3->setText("Default Label 3");
       // ui.lineEdit->setEnabled(true);
       // ui.lineEdit_2->setEnabled(true);
       // break;
    }
     showall();
     ui->label->setText(listdata.at(0));
    ui->label_2->setText(listdata.at(1));
    ui->label_3->setText(listdata.at(2));
    ui->label_4->setText(listdata.at(3));
    ui->label_5->setText(listdata.at(4));
    ui->label_6->setText(listdata.at(5));
    ui->label_7->setText(listdata.at(6));
    ui->label_8->setText(listdata.at(7));
    ui->label_9->setText(listdata.at(8));
    for(int i=0;i<hideshow.size();i++)
    {
        qDebug()<<"list hideshow.at(i)"<<hideshow.at(i)<<endl;
        if(hideshow.at(i)== "com1")
         ui->comboBox_2->hide();
        if(hideshow.at(i)== "com2")
         ui->comboBox_3->hide();
        else if(hideshow.at(i)== "2")
            ui->lineEdit_2->setDisabled(true);
        else if(hideshow.at(i)== "3")
            ui->lineEdit_3->setDisabled(true);
        else if(hideshow.at(i)== "5")
            ui->lineEdit_5->setDisabled(true);
        else if(hideshow.at(i)== "6")
            ui->lineEdit_6->setDisabled(true);
        else if(hideshow.at(i)== "7")
            ui->lineEdit_7->setDisabled(true);
        else if(hideshow.at(i)== "8")
            ui->lineEdit_8->setDisabled(true);
        else if(hideshow.at(i)== "9")
            ui->lineEdit_9->setDisabled(true);

    }

}
void Flow_Area::showall()
{
    ui->lineEdit_2->show();
    ui->lineEdit_3->show();
    ui->comboBox_2->show();
    ui->comboBox_3->show();
    ui->lineEdit_2->setEnabled(true);
    ui->lineEdit_3->setEnabled(true);
    ui->lineEdit_5->setEnabled(true);
    ui->lineEdit_6->setEnabled(true);
    ui->lineEdit_7->setEnabled(true);
    ui->lineEdit_8->setEnabled(true);
    ui->lineEdit_9->setEnabled(true);
}
