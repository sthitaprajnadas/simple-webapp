# Simple Web Application

This is a simple web application using [Python Flask](http://flask.pocoo.org/) and [MySQL](https://www.mysql.com/) database. 
This is used in the demonstration of development of Ansible Playbooks.
  
  Below are the steps required to get this working on a base linux system.
  
  - Install all required dependencies
  - Install and Configure Database
  - Start Database Service
  - Install and Configure Web Server
  - Start Web Server
   
   # Ubuntu
## 1. Install all required dependencies
  
  Python and its dependencies

    apt-get install -y python python-setuptools python-dev build-essential python-pip python-mysqldb

   
## 2. Install and Configure Database
    
 Install MySQL database
    
    apt-get install -y mysql-server mysql-client

## 3. Start Database Service
  - Start the database service
    
        service mysql start

  - Create database and database users
        
        # mysql -u <username> -p
        
        mysql> CREATE DATABASE employee_db;
        mysql> GRANT ALL ON *.* to db_user@'%' IDENTIFIED BY 'Passw0rd';
        mysql> USE employee_db;
        mysql> CREATE TABLE employees (name VARCHAR(20));
        
  - Insert some test data
        
        mysql> INSERT INTO employees VALUES ('JOHN');
    
## 4. Install and Configure Web Server

Install Python Flask dependency

    pip install flask
    pip install flask-mysql

- Copy app.py or download it from source repository
- Configure database credentials and parameters 

## 5. Start Web Server

Start web server

    FLASK_APP=app.py flask run --host=0.0.0.0
    
## 6. Test

Open a browser and go to URL

    http://<IP>:5000                            => Welcome
    http://<IP>:5000/how%20are%20you            => I am good, how about you?
    http://<IP>:5000/read%20from%20database     => JOHN


  # ON AMI LINUX
  
## 1. Install python and dependencies
  sudo yum -y update
  sudo yum -y install gcc openssl-devel bzip2-devel libffi-devel
  
  Download Python  
  
  cd /opt
  sudo wget https://www.python.org/ftp/python/3.7.9/Python-3.7.9.tgz
  sudo tar xzf Python-3.7.9.tgz
  
  Install Python
  
  cd Python-3.7.9
  sudo ./configure --enable-optimizations
  sudo make altinstall
  
  sudo rm ../Python-3.7.9.tgz
## 2. Install and Configure Database
    
  Install MySQL database
    
    sudo yum -y update
    sudo wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
    sudo rpm -Uvh mysql80-community-release-el7-3.noarch.rpm
    sudo yum -y install mysql-server
    sudo systemctl start mysqld
    sudo yum -y install git


    # Check root password
    sudo grep 'password' /var/log/mysqld.log   
    # Change pwd
    sudo mysql_secure_installation
    
  Create MySQL user
    # mysql -u <username> -p

    mysql> CREATE DATABASE employee_db;
    mysql> CREATE USER 'db_user'@'localhost' IDENTIFIED BY 'Passw0rd/12';
    mysql> GRANT ALL PRIVILEGES ON employee_db.* TO 'db_user'@'localhost';
    mysql> USE employee_db;
    mysql> CREATE TABLE employees (name VARCHAR(20));
  
  - Insert some test data
        
    mysql> INSERT INTO employees VALUES ('JOHN');


  ## 4. Install and Configure Web Server

  Install Python Flask dependency

    pip3 install flask
    pip3 install flask-mysql

- Copy app.py or download it from source repository
- Configure database credentials and parameters 

