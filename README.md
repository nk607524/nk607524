#ifndef CUSTOMBUTTON_H
#define CUSTOMBUTTON_H

#include <QPushButton>
#include <QPainter>
#include <QColor>
#include <QPen>
#include <QDebug>

class CustomButton : public QPushButton {
    Q_OBJECT

public:
    explicit CustomButton(QWidget *parent = nullptr);

    void setColor(const QColor &newColor);
    void setGeometry(int x, int y, int w, int h);


protected:
    void paintEvent(QPaintEvent *event) override;

private:
    QColor color;
    int x,y,w,h;

};

#endif // CUSTOMBUTTON_H
#include "CustomButton.h"

CustomButton::CustomButton(QWidget *parent)
    : QPushButton(parent), color(255, 0, 0),x(0), y(0), w(100), h(50)  // Default to red color
{
}

void CustomButton::setColor(const QColor &newColor) {
    color = newColor;
    update(); // Request a repaint
}

void CustomButton::setGeometry(int x, int y, int w, int h) {
    this->x = x;
    this->y = y;
    this->w = w;
    this->h = h;
    update(); // Request a repaint
}


void CustomButton::paintEvent(QPaintEvent *event) {
    QPushButton::paintEvent(event);

   QPushButton::setGeometry(x,y,w,h);

   qDebug()<<"size of data"<<x<<y<<w<<h<<endl;
    QPainter painter(this);
    QPen pen;
    pen.setColor(Qt::black); // Pen color for the rectangle border
    painter.setPen(pen);

    painter.setBrush(color);
    QRect rect(10, 10, 30, 30); // Position and size of the rectangle
   // QRect rect(x,y,w,h);
    painter.drawRect(rect);

    // Draw the RGB values as text
    QString rgbText = QString("RGB(%1, %2, %3)").arg(color.red()).arg(color.green()).arg(color.blue());
    painter.drawText(rect.right() + 15, rect.top() + rect.height() / 2, rgbText); // Position of the text

}

#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include <QPainter>
#include <QPen>
#include "CustomButton.h"
#include <QDebug>
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

private:
    Ui::MainWindow *ui;

};
#endif // MAINWINDOW_H
#include "mainwindow.h"
#include "ui_mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);

    CustomButton *button = new CustomButton(this);
   button->setColor(QColor(0, 255, 0)); // Set the button color to green
   // button->resize(200, 100);

   button->setGeometry(100, 100, 250, 50); // Set the button geometry



}

MainWindow::~MainWindow() {
    delete ui;
}

