#include "TubeFREPropertiesWidget.h"


TubeFREPropertiesWidget::TubeFREPropertiesWidget(QWidget *parent)
	: QWidget(parent)
{
	ui.setupUi(this);
	model = new QStandardItemModel(9, 2, this);///row,coloumn,parent



	model->setItem(0,0, new QStandardItem("Normal Flow Section"));
	model->setItem(1,0, new QStandardItem("Diameter Outer (in)"));
	model->setItem(2,0, new QStandardItem("Thickness Wall (in)"));
	model->setItem(3,0, new QStandardItem("Quantity"));
	model->setItem(4, 0, new QStandardItem("Equivalent Diameter (in)"));
	model->setItem(5, 0, new QStandardItem("Hydraulic Diameter (in)"));
	model->setItem(6, 0, new QStandardItem("Perimeter Wetted(in)"));
	model->setItem(7, 0, new QStandardItem("Area(in-in)"));
	model->setItem(8, 0, new QStandardItem("Total-Area (in-in)"));

	 

	 model1 = new QStandardItemModel(6, 2, this);///row,coloumn,parent

	 model1->setItem(0, 0, new QStandardItem("select a frictional factor correlation  "));
	 model1->setItem(1, 0, new QStandardItem("Enterance Loss (Optional)"));
	 model1->setItem(2, 0, new QStandardItem("Length (Inches)"));
	 model1->setItem(3, 0, new QStandardItem("Roughness Absolute(ft)"));
	 model1->setItem(4, 0, new QStandardItem("Relative Roughness"));
	 model1->setItem(5, 0, new QStandardItem("Moody Friction Factor"));

	 
	 ui.tableView->setModel(model);
	 ui.tableView_2->setModel(model1);

	 // Automatically resize the columns to fit the contents
	 ui.tableView->resizeColumnsToContents();
	 ui.tableView_2->resizeColumnsToContents();


	 // Make the last column stretch to fill the available space
	 ui.tableView->horizontalHeader()->setStretchLastSection(true);
	 ui.tableView_2->horizontalHeader()->setStretchLastSection(true);

	 // Optionally, you can also set the section resize mode for all columns to make them expand automatically
	 ui.tableView->horizontalHeader()->setSectionResizeMode(QHeaderView::Stretch);
	 ui.tableView_2->horizontalHeader()->setSectionResizeMode(QHeaderView::Stretch);

	


	 // Set the size policy and minimum size for tableView1
	 ui.tableView->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);
	 ui.tableView->setMinimumSize(200, 200); // Adjust the minimum size as needed

	 // Set the size policy and minimum size for tableView2
	 ui.tableView_2->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);
	 ui.tableView_2->setMinimumSize(550, 150);
   Delegate *bnr = new Delegate(ui->tableView);
//    ui->tableView->setItemDelegateForColumn(bnr);
//    ui->tableView->setItemDelegateForRow(2,bnr);
    ui->tableView->setItemDelegate(bnr);

	
}


	




TubeFREPropertiesWidget::~TubeFREPropertiesWidget()
{}



#ifndef DELEGATE_H
#define DELEGATE_H
#include <QItemDelegate>
#include <QModelIndex>
#include <QObject>
#include <QStandardItemModel>
#include <QItemDelegate>
#include <QComboBox>
#include <QSpinBox>
#include <QLineEdit>


class Delegate : public QItemDelegate
{
    Q_OBJECT
public:
    Delegate(QObject *parent = nullptr);
    QWidget *createEditor(QWidget *parent, const QStyleOptionViewItem &option, const QModelIndex &index) const override;
        void setEditorData(QWidget *editor, const QModelIndex &index) const override;
            void setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const override;
};

#endif // DELEGATE_H





#include "delegate.h"


Delegate::Delegate(QObject *parent):QItemDelegate(parent)
{

}


QWidget *Delegate::createEditor(QWidget *parent, const QStyleOptionViewItem &option, const QModelIndex &index) const
{
    if (index.row() == 0) {
        if(index.column() == 1)
        {
        QComboBox *comboBox = new QComboBox(parent);
        comboBox->addItems({"Standard Tube", "Naveen", "Option 3","bnr"});
        return comboBox;
        }
    } else if (index.row() == 1) {
        if(index.column() == 1)
        {
        QSpinBox *spinBox = new QSpinBox(parent);
        spinBox->setRange(0, 100);
        return spinBox;
        }
    } else if (index.row() == 2) {
        if(index.column() == 1)
        {
        QLineEdit *lineEdit = new QLineEdit(parent);
        return lineEdit;
        }
    } else {
        return QItemDelegate::createEditor(parent, option, index);
    }
}

void Delegate::setEditorData(QWidget *editor, const QModelIndex &index) const
{
    if (index.row() == 0) {
        if(index.column() == 1)
        {
            QComboBox *comboBox = qobject_cast<QComboBox *>(editor);
            comboBox->setCurrentText(index.model()->data(index, Qt::EditRole).toString());
        }
    } else if (index.row() == 1) {
        if(index.column() == 1)
        {

            QSpinBox *spinBox = qobject_cast<QSpinBox *>(editor);
            spinBox->setValue(index.model()->data(index, Qt::EditRole).toInt());
        }
    } else if (index.row() == 2) {
        if(index.column() == 1)
        {
            QLineEdit *lineEdit = qobject_cast<QLineEdit *>(editor);
            lineEdit->setText(index.model()->data(index, Qt::EditRole).toString());
        }
    } else {
        QItemDelegate::setEditorData(editor, index);
    }
}

void Delegate::setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const
{
    if (index.row() == 0) {
        if(index.column() == 1)
        {
            QComboBox *comboBox = qobject_cast<QComboBox *>(editor);
            model->setData(index, comboBox->currentText(), Qt::EditRole);
        }
    } else if (index.row() == 1) {
        if(index.column() == 1)
        {
            QSpinBox *spinBox = qobject_cast<QSpinBox *>(editor);
            model->setData(index, spinBox->value(), Qt::EditRole);
        }
    } else if (index.row() == 2) {
        if(index.column() == 1)
        {
            QLineEdit *lineEdit = qobject_cast<QLineEdit *>(editor);
            model->setData(index, lineEdit->text(), Qt::EditRole);
        }
    } else {
        QItemDelegate::setModelData(editor, model, index);
    }
}



