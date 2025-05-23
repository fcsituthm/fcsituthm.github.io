---
author: ariffinmzin
categories: [guidelines, fyp]
date: 2025-05-20 19:07:00 +0800
last_modified_at: 2025-05-22 21:03:00 +0800
title: "Step-by-Step Guide: Deploy Your FYP on the Faculty Server"
---




---

## 1. Server Allocation Table

| Program                                                      | Server IP     |
| ------------------------------------------------------------ | ------------- |
| Bachelor of Computer Science (Software Engineering)          | 10.65.200.1   |
| Bachelor of Computer Science (Information Security)          | 10.65.200.5   |
| Bachelor of Computer Science (Web Technology)                | 10.65.200.6   |
| Bachelor of Information Technology                           | 10.65.200.8   |


1. The table above lists each degree program alongside its assigned server IP. Students should use these IPs to deploy their FYPs and to connect to services on the faculty server.
2. These **server IPs are only accessible within the local UTHM network** — either via **UTHM Wi-Fi** or **Eduroam** on campus.
3. The **username and password** for all services (phpMyAdmin, File Browser) is your **matric number**.
4. Access examples to the services:

* phpMyAdmin - To open the database client:

> `https://<server_ip>/phpmyadmin`
>
>_Example: https://10.65.200.1/phpmyadmin_
{: .prompt-info }
* File Browser (no HTTPS) - To upload and manage project files:

> `http://<server_ip>:3000/filebrowser`
>
>_Example: http://10.65.200.1:3000/filebrowser_
{: .prompt-info }

---

## 2. Export Your Local Database

1. **Login** to your local **phpMyAdmin**.  
2. **Select** your project database. _The figure below shows an example of a project database named `webdev_week_10_1_20242025`_.  
![Desktop View](/assets/img/2025-05-20/select_database.png){: w="600" h="300" }
3. Select the **Export** tab, and click **Export** at the bottom.
![Desktop View](/assets/img/2025-05-20/export_database.png){: w="600" h="300" }
4. You will see an `.sql` file has been generated.
![Desktop View](/assets/img/2025-05-20/sql_file.png){: w="600" h="300" }

---

## 3. Import the Database on the Server

1. Browse to `https://<server_ip>/phpmyadmin` and **login**.  
2. If a warning appears, click **Advanced or its equivalent (depending on your browser)**, and then click **Continue**.
![Desktop View](/assets/img/2025-05-20/not_private_2.png){: w="600" h="300" }
![Desktop View](/assets/img/2025-05-20/not_private_3.png){: w="600" h="300" }
3. Enter your login details on the `PhpMyAdmin` login page.
![Desktop View](/assets/img/2025-05-20/phpmyadmin.png){: w="600" h="300" }
4. **Select** your database (named with your matric number).
![Desktop View](/assets/img/2025-05-20/database_matric_number.png){: w="600" h="300" }
5. Go to the **Import** tab. Click **Choose File** and pick the SQL file you exported earlier.  
![Desktop View](/assets/img/2025-05-20/import_database.png){: w="600" h="300" }
6. Click **Import** at the bottom.
7. You will see all the tables under within your database.
![Desktop View](/assets/img/2025-05-20/import_successful.png){: w="600" h="300" }

---

## 4. Upload Your Project Files

1. Open `http://<server_ip>:3000/filebrowser` and **login** using the same login details as previous.
![Desktop View](/assets/img/2025-05-20/filebrowser_login_page.png){: w="600" h="300" }
2. On the landing page, you will see several existing files. **Do not delete them.**
![Desktop View](/assets/img/2025-05-20/filebrowser_landing_page.png){: w="600" h="300" }
3. Click the **Upload Button** at the top-right corner.
![Desktop View](/assets/img/2025-05-20/upload_button.png){: w="600" h="300" }
4. Click **Upload Files**, select all your project files, then **Upload**. Again, click **Upload Folders**, select your directories, then **Upload**.
![Desktop View](/assets/img/2025-05-20/upload_file_folder.png){: w="600" h="300" }
5. Click the **Select Multiple** button if you want to delete one or more files or folders.
![Desktop View](/assets/img/2025-05-20/select_multiple.png){: w="600" h="300" }
6. Double-click any file to open it in the built-in code editor. You can edit and save changes directly within the interface.

---

## 5. Configure Database Connection in Your Code

In your PHP (database connection or config) file, set:

```php
$host     = "localhost";
$db_name  = "yourmatricnumber";
$username = "yourmatricnumber";
$password = "yourmatricnumber";
//please mind that the variable name could be different from yours
```
---

## 6. Access Your Web Application

1. Ensure your entry page is named `index.php` or `index.html`.
2. Visit your deployed application at: `https://<server_ip>/yourmatricnumber`.
3. Done! Your FYP is now live on the faculty server.


> _Tip: You must trust the server’s self-signed certificate in your browser before you can load the site over HTTPS without warnings._
{: .prompt-danger }