**Important**: Do not delete the ibdata1 file. You could destroy all your databases.

First try using the MySQL backup folder which is included with XAMPP. So do next steps:

- Rename folder mysql/data to mysql/data_old
- Make a copy of mysql/backup folder and name it as mysql/data
- Copy all your database folders from mysql/data_old into mysql/data (except mysql, performance_schema, and phpmyadmin folders)
- Copy mysql/data_old/ibdata1 file into mysql/data folder
- Start MySQL from XAMPP control panel.

This is an emergency solution, not a permanent one. After recovering your data is strongly recommended to back it up, and reinstalling XAMPP, 
because the failure is related to a malfunction from some of the files of XAMPP, not the databases.

Collected from : [Stackoverflow](https://stackoverflow.com/a/61859561)
