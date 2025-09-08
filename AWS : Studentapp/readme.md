# $${\color{red} \textbf{Project}: \textbf{Student}  \ \textbf{App}}$$


## 1. Create Security Group and add following ports
- 80 = HTTP
- 22 = SSH 
- 8080 = Tomcat 
- 3306 = Mysql / Mariadb
<img width="1896" height="863" alt="Screenshot 2025-08-29 181629" src="https://github.com/user-attachments/assets/6c9666bf-0ef7-4893-90f7-c68502a5ab76" />


## 2. Launch ec2 instance

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
