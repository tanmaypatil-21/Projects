# $${\color{yellow} \textbf{Project}: \textbf{Student}  \ \textbf{App}}$$


## 1. Create Security Group and add following ports in inbound rule
- 80 = HTTP
- 22 = SSH 
- 8080 = Tomcat 
- 3306 = Mysql / Mariadb
<img width="1896" height="863" alt="Screenshot 2025-08-29 181629" src="https://github.com/user-attachments/assets/6c9666bf-0ef7-4893-90f7-c68502a5ab76" />


## 2. Launch ec2 instance with connect SG 

<img width="1887" height="862" alt="Screenshot 2025-08-29 182250" src="https://github.com/user-attachments/assets/8430c33e-4505-4fc6-9f8b-f775561f62e7" />



## 3. Go to RDS Service and create DB instance

<img width="1902" height="865" alt="Screenshot 2025-08-29 184825" src="https://github.com/user-attachments/assets/b55b13dd-c78e-48fa-b8df-abdd8f2bc79c" />

## 4. Connect instance into Terminus or Mobaxtream

**Download mariadb-server using  below command**

````
yum install mariadb105-server -y
systemctl start mariadb    
systemctl enable mariadb  
systemctl status mariadb
````
<img width="616" height="183" alt="Screenshot 2025-08-29 185413" src="https://github.com/user-attachments/assets/23a3992a-3514-4b22-bd6d-814d84617624" />

## log in into DataBase-instance

````
mysql -h "rds-endpoint"   -u admin -ppassword123
````
<img width="1212" height="27" alt="Screenshot 2025-08-29 185714" src="https://github.com/user-attachments/assets/85acb7c5-9f62-4c81-b540-72dbfdb6ea8b" />

Note: replace rds-endpoint with actual endpoint value and password also

<img width="1897" height="867" alt="Screenshot 2025-08-29 185453" src="https://github.com/user-attachments/assets/b228897e-9665-481b-bcd9-dbe5a3fee9a1" />

## Create database 
````
create database  studentapp;
````
```sql
show databases;
```
````
use studentapp;
````

<img width="503" height="449" alt="Screenshot 2025-08-29 185900" src="https://github.com/user-attachments/assets/6ab8ba04-d775-4311-a22c-ac7160c81326" />

## Create table

```sql
 CREATE TABLE if not exists students(student_id INT NOT NULL AUTO_INCREMENT,  
	student_name VARCHAR(100) NOT NULL,  
	student_addr VARCHAR(100) NOT NULL,   
	student_age VARCHAR(3) NOT NULL,      
	student_qual VARCHAR(20) NOT NULL,     
	student_percent VARCHAR(10) NOT NULL,   
	student_year_passed VARCHAR(10) NOT NULL,  
	PRIMARY KEY (student_id)  
);
```

<img width="1022" height="296" alt="Screenshot 2025-08-29 190100" src="https://github.com/user-attachments/assets/c732b78d-9481-42ed-9467-77239ec5dcb7" />

## Logout from database:
```sql
 exit
```

## 5. Set up Application

### Install Java
````
yum install java-1.8* -y 
````
<img width="539" height="24" alt="Screenshot 2025-08-29 190143" src="https://github.com/user-attachments/assets/274a4425-1f7a-4f3d-b507-12ce8317ecd0" />

### Install tomcat

<img width="1232" height="881" alt="Screenshot 2025-08-29 190329" src="https://github.com/user-attachments/assets/f1f93d0a-e127-4754-b462-06703f8bd4ce" />


````
wget  https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.108/bin/apache-tomcat-9.0.108.zip
````
````
unzip apache-tomcat-9.0.108.zip
````

<img width="1140" height="29" alt="Screenshot 2025-08-29 190556" src="https://github.com/user-attachments/assets/24d43439-255d-4624-92b0-58e4b7ed4bad" />
<img width="608" height="31" alt="Screenshot 2025-08-29 190655" src="https://github.com/user-attachments/assets/1ef7c1f7-08c0-4d07-8fee-a2f2433e8561" />

### Now check file and move into /opt

````
ls
````
````
mv apache-tomcat-9.0.108 /opt
````

<img width="598" height="78" alt="Screenshot 2025-08-29 190859" src="https://github.com/user-attachments/assets/4fb0a1bf-d1fa-467e-a524-a85054f13252" />

### Then go to /opt

````
cd /opt
````
<img width="373" height="56" alt="Screenshot 2025-08-29 191048" src="https://github.com/user-attachments/assets/d7c80018-02e4-44bf-b473-3dfbbe5a8a70" />

### Open tomcat file

````
cd  apache-tomcat-9.0.108
````

### go to webapps directory and paste this link to download student.war

````
curl -O https://s3-us-west-2.amazonaws.com/studentapi-cit/student.war
````
````
cd ..
````

<img width="1308" height="121" alt="Screenshot 2025-08-29 191700" src="https://github.com/user-attachments/assets/60b656bd-c47d-46ee-adda-84e3c70357eb" />

### go to lib directory and paste this link

````
curl -O https://s3-us-west-2.amazonaws.com/studentapi-cit/mysql-connector.jar 
````

<img width="1307" height="104" alt="Screenshot 2025-08-29 191832" src="https://github.com/user-attachments/assets/ccd3b17e-05e1-44a9-8518-3feabf12af5a" />


## Modify context.xml file to setup database connection with database

```
cd /conf
```
````
vim context.xml
````

<img width="1729" height="148" alt="Screenshot 2025-08-29 192021" src="https://github.com/user-attachments/assets/52320735-0df6-4559-8324-03b1b36235b1" />

````
 <Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
               maxTotal="100" maxIdle="30" maxWaitMillis="10000"
               username="USERNAME" password="PASSWORD" driverClassName="com.mysql.jdbc.Driver"
               url="jdbc:mysql://DB-ENDPOINT:3306/DATABASE"/>

````
<img width="1166" height="142" alt="Screenshot 2025-08-29 192422" src="https://github.com/user-attachments/assets/7035b0d0-d061-438e-b730-66293f45f11d" />

* Change  
1.Username  
2.Password   
3.DB-ENDPOINT  
4.DATABASE Name
  

### go to bin dir abd assign +x permission to catalina.sh
````
cd bin
````
````
chmod +x catalina.sh     
````

<img width="1624" height="174" alt="Screenshot 2025-08-29 192822" src="https://github.com/user-attachments/assets/85ff151a-218a-456a-8685-bda5517c9d6d" />


### Start Tomcat
````
sh catalina.sh start
````

<img width="1199" height="211" alt="Screenshot 2025-08-29 192918" src="https://github.com/user-attachments/assets/aa663b4a-aad6-4f20-adbe-59340c6c62f9" />

## 6. go to browser and public ip:8080
<img width="1918" height="985" alt="Screenshot 2025-08-29 193011" src="https://github.com/user-attachments/assets/ad594626-5db6-46d1-8106-8738333c858d" />

### public ip:8080/student
<img width="1918" height="485" alt="Screenshot 2025-08-29 193512" src="https://github.com/user-attachments/assets/f644ac81-96f6-4e75-ac97-8e24a9b725ff" />

<img width="1919" height="266" alt="Screenshot 2025-08-29 193405" src="https://github.com/user-attachments/assets/da61817a-1f24-4298-b96a-6221abee6917" />



