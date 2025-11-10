# stdapp

command
tomcat server (private)
sudo -i root user
sudo apt update && sudo apt upgrade -y
sudo apt install openjdk-17-jdk -y
mkdir /opt/tomcat
tar -xzvf apache-tomcat-9.0.90.tar.gz -C /opt/tomcat
mv student.war /opt/tomcat/apache-tomcat-9.0.90.tar.gz/webapps
mv mysql-connector.jar opt/tomcat/apache-tomcat-9.0.90.tar.gz/lib


database (private) (manual)
sudo apt update && sudo apt upgrade -y
sudo apt install mysql-server -y
sudo systemctl start mysql
sudo systemctl enable mysql
sudo systemctl status mysql
sudo mysql_secure_installation
sudo MySQL
CREATE USER 'admin'@'%' IDENTIFIED BY 'Passwd123';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
exit
enter with user admin and password
show databases;
create database  studentapp;
use studentapp;
 CREATE TABLE if not exists students(student_id INT NOT NULL AUTO_INCREMENT,  
	student_name VARCHAR(100) NOT NULL,  
	student_addr VARCHAR(100) NOT NULL,   
	student_age VARCHAR(3) NOT NULL,      
	student_qual VARCHAR(20) NOT NULL,     
	student_percent VARCHAR(10) NOT NULL,   
	student_year_passed VARCHAR(10) NOT NULL,  
	PRIMARY KEY (student_id)  
);
EXIT;

go to tomcat server
 cd /opt/tomcat/apache/conf
vim context.xml
 make this changes ( <Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
               maxTotal="100" maxIdle="30" maxWaitMillis="10000"
               username="admin" password="Passwd123" driverClassName="com.mysql.jdbc.Driver"
               url="jdbc:mysql://database-1.ccbuq8asm627.us-east-1.rds.amazonaws.com:3306/studentapp"/>

)on line 21

chmod +x catalina.sh
./catalina.sh start

switch to nginx server (public)
sudo apt update && sudo apt upgrade -y
sudo apt install nginx -y
sudo vim /etc/nginx/nginx.conf
location / {
proxy_pass http://10.0.2.4:8080/student/;
}
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx


if we used RDS (with apache)
sudo apt update
sudo apt upgrade -y
sudo apt install mysql-server -y
sudo systemctl start mysql
sudo systemctl enable mysql
sudo systemctl status mysql
sudo mysql_secure_installation
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 0.0.0.0
sudo systemctl restart mysql
mysql -h rds-endpoint   -u admin -pPasswd123 (login with admin user)


