-
void mainview::saveTableData()
{
    QString fileName = QString("honeywell.csv");
    QFile file(fileName);

    if (file.open(QIODevice::WriteOnly)) {
        QTextStream stream(&file);

        // Write header
        for (int col = 0; col < tableModel->columnCount(); ++col) {
            stream << tableModel->headerData(col, Qt::Horizontal).toString();
            if (col < tableModel->columnCount() - 1)
                stream << ",";
        }
        stream << "\n";

        // Write data
        for (int row = 0; row < tableModel->rowCount(); ++row) {
            for (int col = 0; col < tableModel->columnCount(); ++col) {
                stream << tableModel->data(tableModel->index(row, col)).toString();
                if (col < tableModel->columnCount() - 1)
                    stream << ",";
            }
            stream << "\n";
        }

        file.close();
    }
    else {
        QMessageBox::information(this, tr("CSV FILE"), tr("CSV file not found"));
    }
}
