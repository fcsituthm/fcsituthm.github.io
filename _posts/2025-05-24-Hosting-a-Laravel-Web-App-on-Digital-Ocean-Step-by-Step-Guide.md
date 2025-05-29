---
author: ariffinmzin
categories: [guidelines, fyp]
date: 2025-05-23 18:53:00 +0800
last_modified_at: 2025-05-29 21:55:00 +0800
title: "Hosting a Laravel Web App on Digital Ocean: Step by Step Guide"
tags: [laravel, hosting]
---


---
> **⚠️ Read This First — Prerequisites & Mind-set**
>
> This guide is **deliberately hands-on** and mirrors what professional developers do in the real world.  
> **Only continue if you’re comfortable with, or willing to commit to, the following:**
>
> 1. **GitHub repository ready** – your Laravel project **must already live on GitHub** (public).  
> 2. **Basic Linux** – you should know essentials like `cd`, `ls`, `nano`, `chmod`, `chown`, etc.  
> 3. **Payment method** – you will enter a **credit/debit card** to pay small fees at GoDaddy & DigitalOcean (≈ RM30/month combined; you can cancel any time).  
> 4. **Perseverance & curiosity** – expect to troubleshoot and learn; copy-and-paste won’t make you industry-ready.
>
> If that sounds overwhelming, there are easier “one-click” hosting tutorials that you can search on YouTube which abstract all the complexity and technicality for non-IT users - feel free to start there.  
> **Why stick with this tutorial?**  
> • Real **hands-on experience** with VPS provisioning and deployment   
> • Concrete **up-skilling** in Git, SSH and server control panel (CloudPanel)  
> • Exposure to **industry-standard practices** you’ll use on the job   
> • Freedom to **customize and extend** your stack later (domains, CI/CD, server tuning, etc.)  
> • Builds a solid base for your **long-term career** in software engineering & DevOps
{: .prompt-warning }

## 1. Purchase a Domain from GoDaddy

1. Log in or create an account on [GoDaddy](https://www.godaddy.com){:target="_blank" rel="noopener noreferrer"}.
2. During the registration, it will ask you to answer some surveys and followed by filling the payment method.

    ![Desktop View](/assets/img/2025-05-24/surveys.png){: w="600" h="300" }

    ![Desktop View](/assets/img/2025-05-24/payment_method.png){: w="600" h="300" }

3. Use the domain search to find an available domain name. You can pick any domain name ranging from your name, the web application name, stakeholder's name, etc as long it is available.
4. For an FYP project, you can choose a cheap extension like `.online, .store, .co, .site, .xyz,` etc.

    ![Desktop View](/assets/img/2025-05-24/domain_search.png){: w="600" h="300" }

5. Add the domain to your cart and complete the purchase. 
6. Once you have purchased, make sure the **auto renew option is off** to avoid automatic renewal after a year. Skip this step if you wish otherwise.

    ![Desktop View](/assets/img/2025-05-24/auto_renew_off.png){: w="600" h="300" } 

---

## 2. Create a VPS on DigitalOcean (Droplet)

1. Sign up a [Digital Ocean](https://www.digitalocean.com){:target="_blank" rel="noopener noreferrer"} account.
2. In the dashboard, click Create in the top menu, then click Droplet.

    ![Desktop View](/assets/img/2025-05-24/create_droplets.png){: w="600" h="300" }

3. Select a data center region. Choose a region close to you or your users for best performance. In this case **Singapore** region is chosen.

    ![Desktop View](/assets/img/2025-05-24/choose_region.png){: w="600" h="300" }

4. Under **Choose an image**, pick **Ubuntu 24.04 (LTS)**.

    ![Desktop View](/assets/img/2025-05-24/choose_an_image.png){: w="600" h="300" }

5. For the cheapest plan, choose a Basic Droplet with minimal specs. A **1 GB RAM, 1 CPU Droplet (shared CPU)** is sufficient for an FYP Laravel app. This costs **$6 per month (RM25)**. You can always scale up later if needed. Otherwise, you are free to select any plan that suits your budget and requirements.

    ![Desktop View](/assets/img/2025-05-24/choose_size.png){: w="600" h="300" }

6. Skip the **Additional Storage** and **Backups** unless if you need it.
7. Set a root password and enable **Add improved metrics monitoring and alerting (free)**. **Make sure to store your password securely**.
    
    ![Desktop View](/assets/img/2025-05-24/set_root_password.png){: w="600" h="300" }

8. Give your droplet a hostname (e.g., “laravel-app-server”). Then click **Create Droplet**. DigitalOcean will provision your server in about a minute.

    ![Desktop View](/assets/img/2025-05-24/finalize_details.png){: w="600" h="300" }

9. Once created, your Droplet (in this case "laravel-app-server") will have a public IP address (visible in the DigitalOcean dashboard).
    
    ![Desktop View](/assets/img/2025-05-24/laravel_app_server.png){: w="600" h="300" }

---

## 3. Install CloudPanel on the Server

1. On your droplet, click the three dots, choose **Access console**.

    ![Desktop View](/assets/img/2025-05-24/access_console.png){: w="600" h="300" }

2. In the **Droplet Console** menu, click **Launch Droplet Console**.

    ![Desktop View](/assets/img/2025-05-24/droplet_console.png){: w="600" h="300" }

3. A new web browser window will pop out showing the server's terminal.
    
    ![Desktop View](/assets/img/2025-05-24/terminal.png){: w="600" h="300" }

4. Copy the following command and paste it in the terminal.

    ```bash
    apt update && apt -y upgrade && apt -y install curl wget sudo
    ```

5. If an alert as below appears, choose **keep the local version currently installed**, then press **Enter**.

    ![Desktop View](/assets/img/2025-05-24/openssh.png){: w="600" h="300" }

6. Once the process finishes, copy and paste the next command. This command will install CloudPanel – **this can take a few minutes**.

    ```bash
    curl -sS https://installer.cloudpanel.io/ce/v2/install.sh -o install.sh; \
    echo "a3ba69a8102345127b4ae0e28cfe89daca675cbc63cd39225133cdd2fa02ad36 install.sh" | \
    sha256sum -c && sudo DB_ENGINE=MARIADB_11.4 bash install.sh
    ```

7. Once the installation finishes, you will get the URL to the **CloudPanel Web UI**. In this case the URL is https://167.172.67.36:8443. **Yours should be different**. Access the URL through your web browser.

    ![Desktop View](/assets/img/2025-05-24/cloudpanel_installation_finishes.png){: w="600" h="300" }

8. The first time, you’ll see a browser warning about a self-signed SSL certificate – this is expected. Proceed with the unsafe/advanced option to continue.
    
    ![Desktop View](/assets/img/2025-05-24/the_connection_is_not_private.png){: w="600" h="300" }

9. Upon first access, CloudPanel will prompt you to create an Admin account. **Do this immediately**. Fill in your admin credentials as prompted (remember them!), and submit to enter and login the CloudPanel dashboard.
    
    ![Desktop View](/assets/img/2025-05-24/admin_creation.png){: w="600" h="300" }

---

## 4. Use CloudPanel to Set Up Your Laravel Site
1. In the CloudPanel interface, click **Add Sites** button.
2. Since this is a Laravel PHP application, select **Create a PHP Site**.
3. Enter the domain you purchased (e.g., yourdomain.com). If you want the site to primarily use www.yourdomain.com, you can enter that. You may also use a subdomain if you wish (e.g., shop.yourdomain.com, blog.yourdomain.com), etc. In the example below, a subdomain named `myapp` is used.

    ![Desktop View](/assets/img/2025-05-24/new_php_site.png){: w="600" h="300" }

4. Leave the **Site User** and **Site User Password** as it is **or you may change it**. **Make sure to remember or keep it safe**. Lastly, click **Create**.
5. Click **Manage** button. This should show site details and tabs like Vhost, Databases, SSL/TLS, etc.

    ![Desktop View](/assets/img/2025-05-24/sites.png){: w="600" h="300" }

6. Go to the Databases tab for the site. Here, click **Add Database**. Enter a name for your database (e.g., laravel_db) and a new database user (e.g., laravel_user) with a secure password and click **Add Database**. **Make sure to copy the database name, username, and password you just created**. We will put these in Laravel’s `.env` file.

    ![Desktop View](/assets/img/2025-05-24/add_database.png){: w="600" h="300" }
    ![Desktop View](/assets/img/2025-05-24/create_database.png){: w="600" h="300" }

---

## 5. Deploy Laravel Application Code
1. In the terminal, type as below. You will see a folder named after the **Site User** as shown in the image at **Section 4 (Use CloudPanel to Set Up Your Laravel Site), Step 5** above.

    ![Desktop View](/assets/img/2025-05-24/ls_home.png){: w="600" h="300" }

2. Next, type the command below. Replace `ariffinmzin-myapp` with your folder name.

    ```bash
    cd /home/ariffinmzin-myapp/htdocs/
    ```

3. Then type the following command. You will see your application folder. In this case, the application folder name is `myapp.ariffinmzin.com`

    ![Desktop View](/assets/img/2025-05-24/ls_app.png){: w="600" h="300" }

4. Type the command below. Replace `myapp.ariffinmzin.com` with your application folder name.

    ```bash
    cd myapp.ariffinmzin.com/
    ```
5. Once you are in the folder, type the following command.

    ```bash
    rm index.php
    ```
6. Go to your GitHub repository and copy the URL of the repository.

    ![Desktop View](/assets/img/2025-05-24/github_url.png){: w="600" h="300" }

7. Type the following commands (one by one) in the terminal. **Replace any relevant with your folder name and GitHub repository link**.

    ```bash
    git init
    ```
    ```bash
    git config --global --add safe.directory /home/ariffinmzin-myapp/htdocs/myapp.ariffinmzin.com
    # replace ariffinmzin-myapp and myapp.ariffinmzin.com accordingly
    ```
    ```bash
    git remote add origin https://github.com/ariffinmzin/room-reservation-system.git
    # the link above is copied from step 6. replace it with your github repo
    ```
    ```bash
    git pull origin main
    ```

8. The previous commands will clone the repository into a the `myapp.ariffinmzin.com` directory. You can see all the Laravel project's files as in the figure below.

    ![Desktop View](/assets/img/2025-05-24/file_manager.png){: w="600" h="300" }

9. Then, click **Add new file**. **Make sure you are in the correct folder (your Laravel project folder)**.

    ![Desktop View](/assets/img/2025-05-24/add_env.png){: w="600" h="300" }
10. Name the new file as `.env`, then press **Add**.
11. Double click the newly create `.env` file.

    ![Desktop View](/assets/img/2025-05-24/env_file_name.png){: w="600" h="300" }

12. Copy the content of your local `.env` file and paste it on the CloudPanel's File Manager interface. Make the necessary amendments as shown below or equivalent with your project's requirements. Set the `DB_DATABASE`,`DB_USERNAME` and `DB_PASSWORD` similar to the one in **Section 4 (Use CloudPanel to Set Up Your Laravel Site), Step 6** above. Click **Save**.

    ![Desktop View](/assets/img/2025-05-24/env_file_setting.png){: w="600" h="300" }

13. Next, in the terminal, run the following command.

    ```bash
    cd /home/ariffinmzin-myapp/htdocs/myapp.ariffinmzin.com
    # make sure you are in your project's folder
    ```

    ```bash
    composer install
    ```

    > If you see the prompt below, type **Yes**
    > ![Desktop View](/assets/img/2025-05-24/composer_install.png){: w="600" h="300" }

    ```bash
    # Download and install nvm:
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

    # in lieu of restarting the shell
    \. "$HOME/.nvm/nvm.sh"

    # Download and install Node.js:
    nvm install 22

    # Verify the Node.js version:
    node -v # Should print "v22.16.0".
    nvm current # Should print "v22.16.0".

    # Verify npm version:
    npm -v # Should print "10.9.2".
    ```

    ```bash
    npm install
    ```

    ```bash
    php artisan key:generate
    ```

    ```bash
    php artisan migrate
    ```

14. Lastly, set the **Root Directory** to include the `public` folder.

    ![Desktop View](/assets/img/2025-05-24/add_public_folder.png){: w="600" h="300" }

---

## 6. Point Your Domain to the Server (DNS Configuration)
1. Log in to GoDaddy, go to your **My Products > Domains**, and click **Manage DNS** for your domain.
2. In the **DNS Records** section, click **Add New Record**

    ![Desktop View](/assets/img/2025-05-24/add_new_record.png){: w="600" h="300" }

3. Set the record as the figure below, then click **Save**. In this case **Name** is set to `myapp` (subdomain, e.g. `myapp.ariffinmzin.com`), and **value** is your **Digital Ocean Droplet’s IP address**. If you do not use any subdomain, replace **Name** with `@`.

    ![Desktop View](/assets/img/2025-05-24/add_new_record_2.png){: w="600" h="300" }

---

## 7. Acessing Your Laravel's Web Application
1. Access your URL on the browser, in this case `https://myapp.ariffinmzin.com`.
2. If you find the following error, run the following command (**replace `ariffinmzin-myapp` and `myapp.ariffinmzin.com` equivalent to your project**).

    ![Desktop View](/assets/img/2025-05-24/error_1.png){: w="600" h="300" }

    ```bash
    # replace ariffinmzin-myapp with your actual site user
    SITE_USER=ariffinmzin-myapp
    SITE_PATH=/home/$SITE_USER/htdocs/myapp.ariffinmzin.com   # adjust if your folder name differs

    # 1) change ownership so the site user fully owns the project
    chown -R $SITE_USER:$SITE_USER $SITE_PATH

    # 2) grant safe write permissions
    find $SITE_PATH/storage -type d -exec chmod 775 {} \;
    find $SITE_PATH/storage -type f -exec chmod 664 {} \;
    find $SITE_PATH/bootstrap/cache -type d -exec chmod 775 {} \;
    find $SITE_PATH/bootstrap/cache -type f -exec chmod 664 {} \;

    # 3) (optional but recommended) clear and rebuild caches
    sudo -u $SITE_USER bash -c "cd $SITE_PATH && php artisan config:clear && php artisan view:clear && php artisan cache:clear"
    ```

3. Refresh your browser, you will see your web application is up and running.
    
    ![Desktop View](/assets/img/2025-05-24/succeed.png){: w="600" h="300" }

---

## 8. Destroying The Droplet

When your FYP is complete and you no longer need the server, it’s a good idea to destroy your Droplet **to stop billing**. **Warning: this action is irreversible and will permanently erase all data on the Droplet.**

1. In the DigitalOcean dashboard, locate your Droplet (e.g., **laravel-app-server**) and click the **three-dot menu** at the top right of its card. Choose **Destroy** from the dropdown.  

    ![Desktop View](/assets/img/2025-05-24/destroy_droplet.png){: w="600" h="300" }

2. On the **Destroy Droplet** confirmation page, click the **Destroy this Droplet** button to confirm.  
    
    ![Desktop View](/assets/img/2025-05-24/destroy_this_droplet.png){: w="600" h="300" }

> Once destroyed, all data is scrubbed and cannot be recovered.
{: .prompt-danger }

---

## 9. Tips

1. You can access the PhpMyAdmin by clicking the **Manage** button.

    ![Desktop View](/assets/img/2025-05-24/access_phpmyadmin.png){: w="600" h="300" }

2. If you have a new push (changes) on your GitHub repository, you can always update on the server by running the following command in the terminal.

    ```bash
    git pull origin main
    ```
3. You can choose **Resize Droplet** from the three-dot menu to scale up your server’s CPU, memory or disk if you need more resources.

    ![Desktop View](/assets/img/2025-05-24/resize_droplet.png){: w="600" h="300" }