#ifndef TABLEVIEW_H
#define TABLEVIEW_H

#include <QWidget>
#include <QStandardItemModel>
#include <QDebug>

namespace Ui {
class TableView;
}

class TableView : public QWidget
{
    Q_OBJECT

public:
    explicit TableView(QWidget *parent = nullptr);
    ~TableView();
     Ui::TableView *ui;
    QStandardItemModel *model;
private:

};

#endif // TABLEVIEW_H


#include "tableview.h"
#include "ui_tableview.h"

TableView::TableView(QWidget *parent) :
    QWidget(parent),
    ui(new Ui::TableView),model(new QStandardItemModel(10, 10, this))
{
    ui->setupUi(this);

       QStringList horizontalHeaderLabels;
               horizontalHeaderLabels<<"Tube OD \n  (in)"<<"WthK(in)"<<"Length(in)"<<"Theta \n(deqs)"<<"Bend R(in)"<<"Kt Loss";

       model->setHorizontalHeaderLabels(horizontalHeaderLabels);


    for (int row = 0; row < 10; ++row) {
            for (int col = 0; col < 10; ++col) {
                QStandardItem *item = new QStandardItem(" ");
                model->setItem(row, col, item);
            }
        }

        ui->tableView->setModel(model);
        ui->tableView->verticalHeader()->hide();
}

TableView::~TableView()
{
    delete ui;
}

String wstampStatus = "TAMPERED";
                                                    System.out.println("WEIGHING SCALE" + wstampStatus);
                                                    if (DealerLoginBy == 2 || PartialOfflineLogin == 1) {
                                                        temp = receivedStr;

                                                        if (temp != null && temp.contains("YES")) {
                                                            String[] parts = receivedStr.split("[ <>]+");

                                                            System.out.println("macid++++" + parts[1]);
                                                            System.out.println("ws code" + parts[2]);
                                                            databaseHelper.tamperStatus(fpsId, "YES", parts[1], parts[2], "null", "null");
                                                        }


                                                    } else {
                                                        reportTampered(fpsId, "YES", parts[1], parts[2], "null", parts[1]);
                                                    }
                                                    // socket.getOutputStream().write("RECEIVED".getBytes());
                                                } else if (receivedStr.contains("NO")) {
                                                    wstampStatus = "NOTTAMPERED";
                                                    System.out.println("WEIGHING SCALE" + wstampStatus);
                                                }
