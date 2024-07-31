/*************************************pushbutton*****************************/
#ifndef BUTTONDELEGATE_H
#define BUTTONDELEGATE_H

#include <QStyledItemDelegate>
#include <QPushButton>
#include <QApplication>
#include <QPainter>

class ButtonDelegate : public QStyledItemDelegate
{
    Q_OBJECT

public:
    ButtonDelegate(QObject *parent = nullptr);

    QWidget *createEditor(QWidget *parent, const QStyleOptionViewItem &option, const QModelIndex &index) const override;
    void setEditorData(QWidget *editor, const QModelIndex &index) const override;
    void setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const override;
    void updateEditorGeometry(QWidget *editor, const QStyleOptionViewItem &option, const QModelIndex &index) const override;
    void paint(QPainter *painter, const QStyleOptionViewItem &option, const QModelIndex &index) const override;

signals:
    void buttonClicked(const QModelIndex &index) const;


};

#endif // BUTTONDELEGATE_H
#include "buttondelegate.h"

ButtonDelegate::ButtonDelegate(QObject *parent)
    : QStyledItemDelegate(parent)
{
}

QWidget *ButtonDelegate::createEditor(QWidget *parent, const QStyleOptionViewItem &option, const QModelIndex &index) const
{
    QPushButton *button = new QPushButton(parent);
    button->setText("Click Me");
    connect(button, &QPushButton::clicked, this, [=] {
        emit buttonClicked(index);
    });
    return button;
}

void ButtonDelegate::setEditorData(QWidget *editor, const QModelIndex &index) const
{
    // No need to set data for this button delegate
}

void ButtonDelegate::setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const
{
    // No need to set data for this button delegate
}

void ButtonDelegate::updateEditorGeometry(QWidget *editor, const QStyleOptionViewItem &option, const QModelIndex &index) const
{
    editor->setGeometry(option.rect);
}

void ButtonDelegate::paint(QPainter *painter, const QStyleOptionViewItem &option, const QModelIndex &index) const
{
    QStyleOptionButton buttonOption;
    buttonOption.rect = option.rect;
    buttonOption.text = "Click Me";
    QApplication::style()->drawControl(QStyle::CE_PushButton, &buttonOption, painter);
}
/********************************spinbox*****************************/
#ifndef SPINBOXDELEGATE_H
#define SPINBOXDELEGATE_H

#include <QStyledItemDelegate>
#include <QSpinBox>

class SpinBoxDelegate : public QStyledItemDelegate
{
    Q_OBJECT

public:
    explicit SpinBoxDelegate(QObject *parent = nullptr);

    QWidget *createEditor(QWidget *parent, const QStyleOptionViewItem &option, const QModelIndex &index) const override;
    void setEditorData(QWidget *editor, const QModelIndex &index) const override;
    void setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const override;
    void updateEditorGeometry(QWidget *editor, const QStyleOptionViewItem &option, const QModelIndex &index) const override;
};

#endif // SPINBOXDELEGATE_H
#include "spinboxdelegate.h"

SpinBoxDelegate::SpinBoxDelegate(QObject *parent)
    : QStyledItemDelegate(parent)
{
}

QWidget *SpinBoxDelegate::createEditor(QWidget *parent, const QStyleOptionViewItem &option, const QModelIndex &index) const
{
    QDoubleSpinBox *doubleSpinBox = new QDoubleSpinBox(parent);
    doubleSpinBox->setDecimals(2); // Allow two decimal places
    doubleSpinBox->setMinimum(0.2);
    doubleSpinBox->setMaximum(2.2);
    doubleSpinBox->setSingleStep(0.01); // Set the step size for the spinbox
    return doubleSpinBox;
}

void SpinBoxDelegate::setEditorData(QWidget *editor, const QModelIndex &index) const
{
    double value = index.model()->data(index, Qt::EditRole).toDouble();
    QDoubleSpinBox *doubleSpinBox = static_cast<QDoubleSpinBox*>(editor);
    doubleSpinBox->setValue(value);
}

void SpinBoxDelegate::setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const
{
    QDoubleSpinBox *doubleSpinBox = static_cast<QDoubleSpinBox*>(editor);
    doubleSpinBox->interpretText();
    double value = doubleSpinBox->value();
    model->setData(index, value, Qt::EditRole);
}

void SpinBoxDelegate::updateEditorGeometry(QWidget *editor, const QStyleOptionViewItem &option, const QModelIndex &index) const
{
    editor->setGeometry(option.rect);
}



/********************************mainwindow****************************/

#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include "buttondelegate.h"
#include <QStandardItemModel>
#include <QDebug>
#include <QColorDialog>
#include "spinboxdelegate.h"

QT_BEGIN_NAMESPACE
namespace Ui { class MainWindow; }
QT_END_NAMESPACE

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    MainWindow(QWidget *parent = nullptr);
    ~MainWindow();
private slots:
    void handleButtonClicked(const QModelIndex &index);

private:
    Ui::MainWindow *ui;
    QStandardItemModel *model;

};
#endif // MAINWINDOW_H
#include "mainwindow.h"
#include "ui_mainwindow.h"
#include "buttondelegate.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow), model(new QStandardItemModel(4, 2, this))
{
    ui->setupUi(this);

    QStringList horizontalHeaderLabels;
    horizontalHeaderLabels << "Tube OD \n  (in)" << "WthK(in)";

    model->setHorizontalHeaderLabels(horizontalHeaderLabels);
    QStringList NameColumn;
    NameColumn << "Background Color" << "Drawing color" << "Text Label Offset X" << "Text Label Offset Y";

    for (int row = 0; row < 4; ++row) {
        QStandardItem *item = new QStandardItem(NameColumn.at(row));
        model->setItem(row, 0, item);
    }

    SpinBoxDelegate *spinBoxDelegate = new SpinBoxDelegate(this);
       ui->tableView->setItemDelegateForColumn(1, spinBoxDelegate);
     ui->tableView->setItemDelegateForRow(2, spinBoxDelegate); // Set delegate for row 2
         ui->tableView->setItemDelegateForRow(3, spinBoxDelegate); // Set delegate for row 3

    // Set the ButtonDelegate for the second column (index 1)
    ButtonDelegate *buttonDelegate = new ButtonDelegate(this);
    connect(buttonDelegate, &ButtonDelegate::buttonClicked, this, &MainWindow::handleButtonClicked);
    ui->tableView->setItemDelegateForColumn(1, buttonDelegate);

    ui->tableView->setModel(model);
    ui->tableView->verticalHeader()->hide();
    ui->tableView->horizontalHeader()->hide();
    ui->tableView->setColumnWidth(0, 200);

    QStringList Nodelist;
               Nodelist<<"BC Node See"<<"Aero BC Node Size"<<"Free Node Size"<<"Station Node Size";

               for (int row = 0; row < 4; ++row) {

                     QStandardItem *item = new QStandardItem(Nodelist.at(row));
                      model->setItem(row, 0, item);

                 }



     ui->tableView_2->setModel(model);
     ui->tableView_2->verticalHeader()->hide();
     ui->tableView_2->horizontalHeader()->hide();
     ui->tableView_2->setColumnWidth(0,200);

        ui->tableView_2->setItemDelegateForColumn(1, spinBoxDelegate);
}

MainWindow::~MainWindow()
{
    delete ui;
}

void MainWindow::handleButtonClicked(const QModelIndex &index)
{
    qDebug() << "Button in row" << index.row() << "clicked";
    QColor color = QColorDialog::getColor(Qt::white, this, "Select Color");

    if (color.isValid()) {
        // Perform actions based on the selected color
        qDebug() << "Selected color:" << color;
    }
}
