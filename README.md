### $\color{blue} \textbf{Create \ Database \ In \ RDS  }$
- Go To RDS
- Created Database
- Standard create 
- Free tier 
- DB name – database-1 
- Username – admin 
- Password – admin1234
- VPC –  VPC
- Don't Connect to Instance
- Public access – no 
- A.Z. – no preference 
- Create database 
- Edit security group -> Add 3306 port

- connect to instance
- change hostname
  
  ````
   sudo -i
  ````
  ````
  yum install java-11-amazon-corretto.x86_64 -y
  ````

  ````
  yum install maven -y
  ````

   ````
  yum install git -y
  ````

  ````
  sudo wget https://dev.mysql.com/get/mysql80-community-release-el7-5.noarch.rpm
  ````

   ````
  sudo rpm -ivh mysql80-community-release-el7-5.noarch.rpm
  ````
  ````
  sudo yum install mysql-server -y
  ````

  ````
  wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.104/bin/apache-tomcat-9.0.104.zip
  ````

 ````
  unzip apache-tomcat-9.0.104.zip
  ````

 ````
  git clone https://github.com/Pritam-Khergade/student-ui.git
  ````

### $\color{blue} \textbf{Create \ Login \ In \ Database  }$
  
   ````
  mysql -h DATABASE-ENDPOINT -u USERNAME -p PASSWORD
  ````

 Note: replace rds-endpoint with actual endpoint value

````
show databases;
````
````
create database  studentapp;
````
````
use studentapp;
````

````
 CREATE TABLE if not exists students(student_id INT NOT NULL AUTO_INCREMENT,  
	student_name VARCHAR(100) NOT NULL,  
	student_addr VARCHAR(100) NOT NULL,   
	student_age VARCHAR(3) NOT NULL,      
	student_qual VARCHAR(20) NOT NULL,     
	student_percent VARCHAR(10) NOT NULL,   
	student_year_passed VARCHAR(10) NOT NULL,  
	PRIMARY KEY (student_id)  
);
````
````
show tables;
````
Logout from database:
````
exit
````

````
cd apache-tomcat-9.0.90.tar.gz/lib
````

````
wget https://s3-us-west-2.amazonaws.com/studentapi-cit/mysql-connector.jar
````

````
cd ..
````

### $\color{blue} \textbf{ MODIFY \ context.xml:}$

````
cd conf
````
````
vim context.xml
````

add below line [connection string] at line 21
````
 <Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
               maxTotal="100" maxIdle="30" maxWaitMillis="10000"
               username="USERNAME" password="PASSWORD" driverClassName="com.mysql.jdbc.Driver"
               url="jdbc:mysql://DB-ENDPOINT:3306/DATABASE-NAME"/>

````
````
cd ../bin
````
````
bash catalina.sh start
````
````
cd student-ui
````
````
mvn clean package
````
````
cd
````
### $\color{blue} \textbf{Copy \ SNAPSHOTFile \ In \ Apache-tomcat/webapps  }$

````
cp /student-ui/target/SNAPSHOT /root/apache-tomcat-9.0.90/webapps
````

### $\color{blue} \textbf{Restart \ Catalina.sh  }$

````
cd apache-tomcat-9.0.90/bin
````
````
bash catalina.sh stop
````
````
bash catalina.sh start
````







