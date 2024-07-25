#pragma once

#include <QWidget>
#include <QStringList>
#include <QDebug>
#include "ui_Flow_Area.h"
#include "Util.h"  // Include this if it contains en_FlowSectionType enum

class Flow_Area : public QWidget
{
    Q_OBJECT

public:
    Flow_Area(QWidget* parent = nullptr);
    ~Flow_Area();

    // Struct with an enum inside
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

        // Getter for the enum type
        en_FlowSectionType getType() const {
            return L_flowAreaType;
        }

        // Setter for the enum type
        void setType(en_FlowSectionType newType) {
            L_flowAreaType = newType;
        }

        QString getLabel1Text() 
        {
            return l_strLabel1;
        }

        QString getLabel2Text()
        {
            return l_strLabel2;
        }
        QString getLabel3Text()
        {
            return l_strLabel3;
        }

        void setLabel1Text(QString p_strLabel1)
        {
            l_strLabel1 = p_strLabel1;
        }

        void setLabel2Text(QString p_strLabel2)
        {
            l_strLabel2 = p_strLabel2;
        }

        void setLabel3Text(QString p_strLabel3)
        {
            l_strLabel3 = p_strLabel3;
        }

        bool isCombo1Enabled()
        {
            return l_bCombo1Enabled;
        }

        bool isCombo2Enabled()
        {
            return l_bCombo2Enabled;
        }

        bool isEdit1Enabled()
        {
            return l_bEdit1Enabled;
        }

        bool isEdit2Enabled()
        {
            return l_bEdit2Enabled;
        }

        void setEdit1Enabled(bool p_bEdit1Enabled)
        {
            l_bEdit1Enabled = p_bEdit1Enabled;
        }

        void setEdit2Enabled(bool p_bEdit2Enabled)
        {
            l_bEdit2Enabled = p_bEdit2Enabled;
        }


    };

    FlowTypeLabel flowArea;
    void showall();
    QStringList hideshow;

private slots:
    void onComboBoxChanged(int index);

private:
    Ui::Flow_AreaClass ui;
    QStringList getEnumStringList() const;
    en_FlowSectionType indexToEnum(int index) const;
    void updateUI(en_FlowSectionType type);

    FlowTypeLabel getLabels(en_FlowSectionType p_enFlowSectionType);

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
    case STANDARD_DRILL:
        showall();
        listdata << "Normal Flow Section" << "Diameter \n Inches(in)" << "Dril Set" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area(in-in)";
        hideshow << "1" << "2" << "3" << "8" << "4" << "5" << "6" << "7";        break;
    case CIRCLE:
        showall();
        listdata << "Normal Flow Section" << " Diameter \n  Inches" << "Radius \n  Inches"  << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "3" << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case AXIAL_GAP:
        showall();
        listdata << "Normal Flow Section" << " Diameter \n  Inches" << "Axial Gap \n  Inches" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\ (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case RADIAL_GAP_DO:
        showall();
        listdata << "Normal Flow Section" << " Diameter \n Outer(in)" << "Radial Gap (in)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case RADIAL_GAP_DI:
        showall();
        listdata << "Normal Flow Section" << " Diameter \n Inner(in)" << "Radial Gap (in)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case RADIAL_GAP_DAVG:
        showall();
        listdata << "Normal Flow Section" << " Diameter \n Mean(in)" << "Radial Gap (in)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case ANNULUS:
        showall();
        listdata << "Normal Flow Section" << " Diameter \n Outer(in)" << "Diameter \n Inner(in)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case RECTANGLE:
        showall();
        listdata << "Normal Flow Section" << " Width (inches)" << "Length\n  (inches)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case SQUARE:
        showall();
        listdata << "Normal Flow Section" << " Side\n  (inches)" << "Equivalent \n Radius (in)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case ROUND_SLOT_CC:
        showall();
        listdata << "Normal Flow Section" << " Width (inches)" << "Length\n  (inches)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case ROUND_SLOT_EE:
        showall();
        listdata << "Normal Flow Section" << " Width (inches)" << "Length\n  (inches)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case ELLIPSE:
        showall();
        listdata << "Normal Flow Section" << " Major Diameter \(in)" << "Minor Diameter\n  (in)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case SEMI_CIRCLE:
        showall();
        listdata << "Normal Flow Section" << " Diameter \n  Inches" << "Radius \n  Inches" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in-in)" << "Total Area\  (in-in)";
        hideshow <<"3" << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case CIRCULAR_SECTOR:
        showall();
        listdata << "Normal Flow Section" << " Diameter \n  Inches" << "Angle \n(degrees)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in - in)" << "Total Area\  (in - in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case RIGHT_TRAINGLE:
        showall();
        listdata << "Normal Flow Section" << "Base  (inches)" << "Height (inches)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in - in)" << "Total Area\  (in - in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case ISOSCELES_TRIANGLE:
        showall();
        listdata << "Normal Flow Section" << "Base  (inches)" << "Height (inches)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in - in)" << "Total Area\  (in - in)";
        hideshow << "4" << "5" << "6" << "8" << "7" << "com1" << "com2";        break;
    case DH_PERIMETER:
        showall();
        listdata << "Normal Flow Section" << " Equivalent Circ \n    Gap(in)" << "Equivalent \n Radius (in)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in - in)" << "Total Area\  (in - in)";
        hideshow << "3" << "9"  << "6" << "8" << "7" << "com1" << "com2";        break;
    case DH_AREA:
        showall();
        listdata << "Normal Flow Section" << " Equivalent Circ \n    Gap(in)" << "Equivalent \n Radius (in)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in - in)" << "Total Area\  (in - in)";
        hideshow << "3" << "4" <<"5" << "9" << "8" << "7" << "9" << "com1" << "com2";        break;
    case PERIMETER_AREA:
        showall();
        listdata << "Normal Flow Section" << " Equivalent Circ \n    Gap(in)" << "Equivalent \n Radius (in)" << "Quantity" << "Equivalent \n Daimeter(in)" << "Hydraulic \n Diameter(in)" << "Permeter \nWetted(in)" << "Area(in - in)" << "Total Area\  (in - in)";
        hideshow << "3" << "4" << "9" << "8" << "7" << "9" << "com1" << "com2";        break;

    }
    showall();

    Flow_Area::FlowTypeLabel l_Labels = getLabels(type);



    //ui.label->setText(listdata.at(0));
    ui.label_2->setText(l_Labels.getLabel1Text());
    ui.label_3->setText(l_Labels.getLabel2Text());
    ui.label_4->setText(l_Labels.getLabel3Text());
    ui.label_5->setText(listdata.at(4));
    ui.label_6->setText(listdata.at(5));
    ui.label_7->setText(listdata.at(6));
    ui.label_8->setText(listdata.at(7));
    ui.label_9->setText(listdata.at(8));
    for (int i = 0; i < hideshow.size(); i++)
    {
        ui.comboBox_2->setDisabled(!l_Labels.isCombo1Enabled());
        ui.comboBox_3->setDisabled(!l_Labels.isCombo2Enabled());

        ui.lineEdit_2->setDisabled(!l_Labels.isEdit1Enabled());
        ui.lineEdit_3->setDisabled(!l_Labels.isEdit2Enabled());

        qDebug() << "list hideshow.at(i)" << hideshow.at(i) << endl;
        if (hideshow.at(i) == "com1")
            ui.comboBox_2->hide();
        if (hideshow.at(i) == "com2")
            ui.comboBox_3->hide();
        else if (hideshow.at(i) == "2")
            ui.lineEdit_2->hide();

        else if (hideshow.at(i) == "3")
            ui.lineEdit_2->setDisabled(true);

        else if (hideshow.at(i) == "4")
            ui.lineEdit_4->setDisabled(true);
        else if (hideshow.at(i) == "5")
            ui.lineEdit_5->setDisabled(true);
        else if (hideshow.at(i) == "6")
            ui.lineEdit_6->setDisabled(true);
        else if (hideshow.at(i) == "7")
            ui.lineEdit_7->setDisabled(true);
        else if (hideshow.at(i) == "1")
            ui.lineEdit->hide();
        else if (hideshow.at(i) == "8")
            ui.lineEdit_3->setDisabled(true);
        else if (hideshow.at(i) == "9")
            ui.lineEdit->setDisabled(true);


    }

}
Flow_Area::FlowTypeLabel Flow_Area::getLabels(en_FlowSectionType p_enFlowSectionType)
{
    FlowTypeLabel l_FlowTypeLabel;
    switch (p_enFlowSectionType)
    {
        case STANDARD_DRILL:
        {
            l_FlowTypeLabel.setLabel1Text("Diameter Inches(in)");
            l_FlowTypeLabel.setLabel2Text("Diameter Inner(in)");

            l_FlowTypeLabel.setEdit1Enabled(false);
            l_FlowTypeLabel.setEdit2Enabled(false);
            break;
        }
    }
    return l_FlowTypeLabel;
}
void Flow_Area::showall()
{
    ui.lineEdit->show();

    ui.lineEdit_2->show();
    ui.lineEdit_3->show();
    ui.comboBox_2->show();
    ui.comboBox_3->show();
    ui.lineEdit->setEnabled(true);

    ui.lineEdit_2->setEnabled(true);
    ui.lineEdit_3->setEnabled(true);
    ui.lineEdit_4->setEnabled(true);

    ui.lineEdit_5->setEnabled(true);
    ui.lineEdit_6->setEnabled(true);
    ui.lineEdit_7->setEnabled(true);
}
