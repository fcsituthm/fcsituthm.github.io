---
author: ariffinmzin
categories: [guidelines, fyp]
date: 2025-05-20 19:07:00 +0800
title: "Step-by-Step Guide: Deploy Your FYP on the Faculty Server"
---




---

## 1. Export Your Local Database

1. **Login** to your local **phpMyAdmin**.  
2. **Select** your project database. _The figure below shows an example of a project database named `webdev_week_10_1_20242025`_.  
![Desktop View](/assets/img/2025-05-20/select_database.png){: w="600" h="300" }
3. Select the **Export** tab, and click **Export** at the bottom.
![Desktop View](/assets/img/2025-05-20/export_database.png){: w="600" h="300" }
4. You will see an `.sql` file has been generated.
![Desktop View](/assets/img/2025-05-20/sql_file.png){: w="600" h="300" }

---

## 2. Import the Database on the Server

1. Browse to `http://10.65.200.7/phpmyadmin` and **login**.  
2. **Select** your database (named with your matric number).  
3. Go to the **Import** tab.  
4. Click **Choose File** and pick the SQL file you exported earlier.  
5. Click **Go** to import.

---

## 3. Upload Your Project Files

1. Open `http://10.65.200.7:3000/filebrowser` and **login**.  
2. Click **Upload Files**, select all your project files, then **Upload**.  
3. Click **Upload Folders**, select your directories, then **Upload**.

---

## 4. Configure Database Connection in Your Code

In your PHP (database connection or config) file, set:

```php
$host     = "localhost";
$db_name  = "yourmatricnumber";
$username = "yourmatricnumber";
$password = "yourmatricnumber";
//please mind that the variable name could be different from yours
```

## 5. Access Your Web Application

1. Ensure your entry page is named `index.php` or `index.html`.
2. Visit your deployed application at: `https://10.65.200.7/yourmatricnumber`.
3. Done! Your FYP is now live on the faculty server.


> _Tip: You must trust the server’s self-signed certificate in your browser before you can load the site over HTTPS without warnings._
{: .prompt-danger }

