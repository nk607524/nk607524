#pragma once

#include <QtWidgets/QMainWindow>
#include "ui_image.h"

class image : public QMainWindow
{
    Q_OBJECT

public:
    image(QWidget *parent = nullptr);
    ~image();

private:
    Ui::imageClass ui;
};



#include "image.h"

image::image(QWidget *parent)
    : QMainWindow(parent)
{
    ui.setupUi(this);
}

image::~image()
{}

