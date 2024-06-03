#include "MainWindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
{
    ui.setupUi(this);
   
  
   
    tableModel = new QStandardItemModel(this);
    tableModel2 = new QStandardItemModel(this);
    ui.actionwidgets1->setCheckable(true);
    ui.actionwidgets1->setChecked(true);
    ui.actionwidgets2->setCheckable(true);
    ui.actionwidgets1->setChecked(true);


    // Connect actions to slots
    connect(ui.actionNew, &QAction::triggered, this, &MainWindow::onNewClicked);
    connect(ui.actionOpen, &QAction::triggered, this, &MainWindow::onOpenClicked);
    connect(ui.actionSave, &QAction::triggered, this, &MainWindow::onSaveClicked);
    connect(ui.actionwidgets1, &QAction::toggled, this, &MainWindow::onWidgetToggled);
    connect(ui.actionwidgets2, &QAction::toggled, this, &MainWindow::onWidgetToggled);
    connect(ui.actionsynchronize, SIGNAL(toggled(bool)), this, SLOT(synchronize_both_table()));


    // Initially hide child widgets
    ui.widget->show();
    ui.widget_2->show();
    ui.pushButton->setEnabled(false);
    ui.pushButton_2->setEnabled(false);

   /* connect(tableModel, &QStandardItemModel::dataChanged, this, &MainWindow::syncItemFromTable1);*/
   /* connect(tableModel2, &QStandardItemModel::dataChanged, this, &MainWindow::syncItemFromTable2);*/
    connect(ui.pushButton, SIGNAL(clicked(bool)), this, SLOT(saveTableData()));
    connect(ui.pushButton_2, SIGNAL(clicked(bool)), this, SLOT(saveTableDatatabe2()));

}

MainWindow::~MainWindow()
{}

void MainWindow::onWidgetToggled(bool checked)
{
    QAction* action = qobject_cast<QAction*>(sender());
    if (action == ui.actionwidgets1) {
        ui.widget->setVisible(checked);
    }
    else if (action == ui.actionwidgets2) {
        ui.widget_2->setVisible(checked);
    }
}




void MainWindow::onNewClicked()
{
    bool ok;
    QString text;
    text = QInputDialog::getText(this, tr("Table 1"), tr("Enter row and column  fromat 1.4"), QLineEdit::Normal, "", &ok);
    if (ok == false)
    {
        QMessageBox::information(this, tr("ERROR"), tr("Don't want row and column"));
    }
    else if (text.isEmpty() && ok == true)
    {
        QMessageBox::information(this, tr("ERROR"), tr("Your not enter any row and column"));
    }
    else {
        QStringList list = text.split(".");
        if (list.size() == 2)
        {
            tablerow = list.at(0);
            tablecolumn = list.at(1);
            if (tablerow.toInt(0) >= 1)
            {
                if (tablecolumn.toInt(0) >= 1)
                {
                    tableModel->setRowCount(tablerow.toInt());
                    tableModel->setColumnCount(tablecolumn.toInt());

                    for (int i = 0; i < tablerow.toInt(0); i++)
                    {
                        for (int j = 0; j < tablecolumn.toInt(0); j++)
                        {
                            QString data = QString(" ").arg(i).arg(j);

                            QModelIndex index = tableModel->index(i, j, QModelIndex());

                            tableModel->setData(index, QVariant::fromValue(data));
                        }
                    }
                    ui.tableView->setModel(tableModel);

                    tableModel2->setRowCount(tablerow.toInt());
                    tableModel2->setColumnCount(tablecolumn.toInt());

                    for (int i = 0; i < tablerow.toInt(0); i++)
                    {
                        for (int j = 0; j < tablecolumn.toInt(0); j++)
                        {
                            QString data = QString(" ").arg(i).arg(j);

                            QModelIndex index = tableModel2->index(i, j, QModelIndex());    //rows,coloumns,parentwindows

                            tableModel2->setData(index, QVariant::fromValue(data));
                        }
                    }
                    ui.tableView_2->setModel(tableModel2);

                }
                else
                    QMessageBox::information(this, tr("ERROR"), tr("Enter correct column number"));
            }
            else
                QMessageBox::information(this, tr("ERROR"), tr("Enter correct row number"));

        }
        else
            QMessageBox::information(this, tr("ERROR"), tr("Enter correct row number  and column number"));

    }
}

void MainWindow::onOpenClicked()
{
    QString fileName = QFileDialog::getOpenFileName(this, tr("Open File"), "", tr("All Files (*)"));
    if (!fileName.isEmpty()) {
        QMessageBox::information(this, tr("File Opened"), tr("File: %1").arg(fileName));
    }
}

void MainWindow::onSaveClicked()
{
    QString fileName = QFileDialog::getSaveFileName(this, tr("Save File"), "", tr("All Files (*)"));
    if (!fileName.isEmpty()) {
        QMessageBox::information(this, tr("File Saved"), tr("File: %1").arg(fileName));
    }
}

void MainWindow::syncItemFromTable1(const QModelIndex& index)
{
    ui->tableView_2->setModel(tableModel);   //naveen

}
void MainWindow::on_tableView_clicked(const QModelIndex &index) //naveen
{
    if(ui->actionsynchronize->isChecked())
    {
     connect(tableModel, &QStandardItemModel::dataChanged, this, &MainWindow::syncItemFromTable1);
    }
}


void MainWindow::syncItemFromTable2(const QModelIndex& index)
{
    int newdata1 = tableModel2->data(index, Qt::EditRole).toInt(0);
}



void MainWindow::saveTableData()
{
    QString fileName = QString("C:\Widges\MainWindow\MainWindow\honeywell.csv");
    QFile file(fileName);

    if (file.open(QIODevice::WriteOnly)) {
        QTextStream stream(&file);
        qDebug() << "where its is naveen222" << Qt::endl;
        for (int col = 0; col < tableModel->columnCount(); ++col) {
            stream << tableModel->headerData(col, Qt::Horizontal).toString();
            if (col < tableModel->columnCount() - 1)
                stream << ",";
        }
        stream << "\n";

        for (int row = 0; row < tableModel->rowCount(); ++row) {
            for (int col = 0; col < tableModel->columnCount(); ++col) {
                stream << tableModel->data(tableModel->index(row, col)).toString();

                if (col < tableModel->columnCount() - 1)
                    stream << ",";
            }
            stream << "\n";
        }

        file.close();
        qDebug() << "it was closed hapeen naveen" << Qt::endl;
    }
    else {
        QMessageBox::information(this, tr("CSV FILE"), tr("CSV file not fount"));

    }
}
void MainWindow::saveTableDatatabe2()
{
    QString fileName = QString("naveen.csv");
    QFile file(fileName);

    if (file.open(QIODevice::WriteOnly)) {
        QTextStream stream(&file);

        for (int col = 0; col < tableModel2->columnCount(); ++col) {
            stream << tableModel2->headerData(col, Qt::Horizontal).toString();
            if (col < tableModel2->columnCount() - 1)
                stream << ",";
        }
        stream << "\n";

        for (int row = 0; row < tableModel2->rowCount(); ++row) {
            for (int col = 0; col < tableModel2->columnCount(); ++col) {
                stream << tableModel2->data(tableModel2->index(row, col)).toString();

                if (col < tableModel2->columnCount() - 1)
                    stream << ",";
            }
            stream << "\n";
        }

        file.close();
    }
    else {
        QMessageBox::information(this, tr("CSV FILE"), tr("CSV file not fount"));

    }
}

void MainWindow::synchronize_both_table()
{

    if (ui.actionsynchronize->isChecked()) {
        qDebug() << "where its hapeen naveen" << Qt::endl;

        ui.pushButton->setEnabled(true);
        ui.pushButton_2->setEnabled(true);

        saveTableData();
        QString pathName = ("C:\Widges\MainWindow\MainWindow\honeywell.csv");

        QStandardItemModel* model = readCSVFile(pathName);
        if (model) {

            ui.tableView_2->setModel(model);
           
        }

    }
    else
    {
        ui.pushButton->setDisabled(true);
        ui.pushButton_2->setDisabled(true);
    }
}
QStandardItemModel* MainWindow::readCSVFile(QString& filePath)
{
    QFile file(filePath);
    if (!file.open(QIODevice::ReadOnly | QIODevice::Text)) {
        return nullptr;
    }

    QStandardItemModel* model = new QStandardItemModel();
    QTextStream in(&file);

    bool isHeader = true;
    while (!in.atEnd()) {
        QString line = in.readLine();
        QList<QStandardItem*> items;
        for (const QString& cell : line.split(',')) {
            items.append(new QStandardItem(cell));
        }
        if (isHeader) {
            model->setHorizontalHeaderLabels(line.split(','));
            isHeader = false;
        }
        else {
            model->appendRow(items);
        }
    }

    file.close();
    return model;
}
