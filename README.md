#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include <QColor>
#include <QPushButton>

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
    void on_pushButton_clicked();

private:
    Ui::MainWindow *ui;
    void drawOnButton(QPushButton *button, const QColor &color);
    QColor color;
};
#endif // MAINWINDOW_H

#include "mainwindow.h"
#include "ui_mainwindow.h"
#include <QColorDialog>
#include <QPixmap>
#include <QPainter>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);
    color = QColor(0, 255, 0); // Default color
       drawOnButton(ui->pushButton, color); // Draw on button initially

       // Connect the button's clicked signal to the slot
       connect(ui->pushButton, &QPushButton::clicked, this, &MainWindow::on_pushButton_clicked);
}

MainWindow::~MainWindow()
{
    delete ui;
}
void MainWindow::drawOnButton(QPushButton *button, const QColor &color)
{
    // Create a QPixmap with the same size as the button

       QPixmap pixmap(button->size());
       pixmap.fill(Qt::transparent); // Start with a transparent background

       QPainter painter(&pixmap);
       painter.setPen(Qt::black); // Pen color for the rectangle border
       painter.setBrush(color); // Brush color for the rectangle fill

       // Rectangle dimensions
       int rectWidth = pixmap.width() / 4; // Width of the rectangle
       int rectHeight = pixmap.height() / 2; // Height of the rectangle

       // Calculate position
       int x = 0; // X-coordinate for the left side
       int y = (pixmap.height() - rectHeight) / 2; // Center the rectangle vertically

       // Draw the rectangle
       painter.drawRect(x, y, rectWidth, rectHeight);

       // Draw the RGB values as text
       QString rgbText = QString("RGB(%1, %2, %3)").arg(color.red()).arg(color.green()).arg(color.blue());
       painter.setPen(Qt::black); // Set text color
       painter.drawText(pixmap.rect().adjusted(rectWidth, rectHeight-10, -10, -10), rgbText); // Draw the text

       // Set the pixmap as the button's icon
       button->setIcon(QIcon(pixmap));
       button->setIconSize(button->size()); // Ensure the icon size matches the button size

}

void MainWindow::on_pushButton_clicked()
{
    QColor selectedColor = QColorDialog::getColor(color, this, "Select Color");

    if (selectedColor.isValid()) {
        color = selectedColor;
        drawOnButton(ui->pushButton, color); // Redraw the button with the new color
    }
}

