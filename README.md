#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include <QStandardItemModel>
#include "delegate.h"

QT_BEGIN_NAMESPACE
namespace Ui { class MainWindow; }
QT_END_NAMESPACE

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    MainWindow(QWidget *parent = nullptr);
    ~MainWindow();

private:
    Ui::MainWindow *ui;
    QStandardItemModel *model;

};
#endif // MAINWINDOW_H


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


#include "mainwindow.h"
#include "ui_mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);
    model = new QStandardItemModel(4,2,this);
    for(int row =0 ;row <4 ; ++row)
    {
        for(int col = 0;col <2;++col)
        {
            QModelIndex index = model->index(row,col,QModelIndex());
            model->setData(index,0);

        }
    }
    ui->tableView->setModel(model);
    Delegate *bnr = new Delegate(ui->tableView);
//    ui->tableView->setItemDelegateForColumn(bnr);
//    ui->tableView->setItemDelegateForRow(2,bnr);
    ui->tableView->setItemDelegate(bnr);
}

MainWindow::~MainWindow()
{
    delete ui;
}


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
        comboBox->addItems({"Option 1", "Option 2", "Option 3"});
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



