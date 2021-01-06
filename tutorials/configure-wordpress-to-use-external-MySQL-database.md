By default, the WordPress chart installs MariaDB on a separate pod inside the cluster and uses it as the WordPress database. We want to disable this behavior and configure WordPress to use an external MySQL database. This and other configuration options (such as the default WordPress admin user and password) can be set at installation time, either via command-line parameters or via a separate YAML configuration file.

In order to keep things organized and easily extendable, we are going to use a configuration file.

Configuring MySQL:
First, we’ll create a dedicated MySQL user and a database for WordPress, allowing connections from external hosts. This is necessary because our WordPress installation will live on a separate server inside the Kubernetes cluster. In case you already have a dedicated MySQL user and database set up for WordPress, you can skip to the next step.

From the MySQL server, log into MySQL with the following command:


mysql -u root -p
 
You will be prompted to provide the password you set up for the root MySQL account when you first installed the software. After logging in, MySQL will give you a command prompt you can use to create the database and user we need for WordPress.

To create the database, you can use the following statement:

CREATE DATABASE wordpress;
 
Now, let’s create a dedicated MySQL user for this database:

CREATE USER wordpress_user IDENTIFIED BY 'password';
 
The user wordpress_user was created, but it doesn’t have any access permissions yet. The following command will give this user admin access (all privileges) to the wordpress database from both local and external networks:

GRANT ALL PRIVILEGES ON wordpress.* TO wordpress_user@'%';
 
To update the internal MySQL tables that manage access permissions, use the following statement:

FLUSH PRIVILEGES;
 
Now you can exit the MySQL client with:

exit;
 
To test that the changes were successful, you can log into the MySQL command-line client again, this time using the new account wordpress_user to authenticate:

mysql -u wordpress_user -p
 
You should use the same password you provided when creating this MySQL user with the CREATE_USER statement. To confirm your new user has access to the wordpress database, you can use the following statement:

show databases;
 
The following output is expected:

Output
+--------------------+
| Database           |
+--------------------+
| information_schema |
| wordpress          |
+--------------------+
2 rows in set (0.03 sec)
After confirming the wordpress database is included in the results, you can exit the MySQL command-line client with:

exit;
 
You now have a dedicated MySQL database for WordPress, and valid access credentials to use within it. Because our WordPress installation will live on a separate server, we still need to edit our MySQL configuration to allow connections coming from external hosts.

While still on your MySQL server, open the file /etc/mysql/mysql.conf.d/mysqld.cnf using your command-line editor of choice:

sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
 
Locate the bind-address setting within this file. By default, MySQL listens only on 127.0.0.1 (localhost). In order to accept connections from external hosts, we need to change this value to 0.0.0.0. This is how your bind-address configuration should look:

/etc/mysql/mysql.conf.d/mysqld.cnf
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address            = 0.0.0.0
 
When you’re done making these changes, save and close the file. You’ll need to restart MySQL with the following command:

sudo systemctl restart mysql
 
To test if you’re able to connect remotely, run the following command from your local machine or development server:

mysql -h mysql_server_ip -u wordpress_user -p
 
Remember to change mysql_server_ip to your MySQL server IP address or hostname. If you’re able to connect without errors, you are now ready to proceed to the next step.