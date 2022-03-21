# Vehicle Service
Vehicle service endpoint.

## Tasks
- Create new SQL script file with file name 'V01__Initial_Setup.sql' at directory /resources/db/migration.
- Create database definition language (DDL) as per following structure:-
	**vehicle:**
	| # | Column Name | Type | Not Null | Other Attributes |
	| --- | --- | --- | --- | --- |
	| 1 | id | int | Y | AUTO_INCREMENT; Primary Key | 
	| 2 | carplate_num | varchar(10) | Y |  |
	| 3 | make | varchar(50) | Y |  |
	| 4 | model | varchar(50) | Y |  |
	| 5 | chassis_num | varchar(60) | Y |  |
	| 6 | axles_num | int | Y |  |
	| 7 | tyre_num | int | Y |  |
	| 8 | roadtax_expiry | varchar(10) | Y |  |
	| 9 | manufacture_year | varchar(4) | Y |  |


	**summon:**
	| # | Column Name | Type | Not Null | Other Attributes |
	| --- | --- | --- | --- | --- |
	| 1 | id | int | Y | AUTO_INCREMENT; Primary Key | 
	| 2 | vehicle_id | int | Y | Foreign key to vehicle table |
	| 3 | serial_num | varchar(10) | Y |  |
	| 4 | fine_amt | double(5,2) | Y |  |
	| 5 | location_ | varchar(60) | Y |  |
	| 6 | officer_name | varchar(60) | Y |  |

- Save the script file.
- Sample for reference 
	```
		create table vehicle (
			id int not null AUTO_INCREMENT,
			carplate_num varchar(10) not null,
			make varchar(50) not null,
			model varchar(50) not null,
			chassis_num varchar(60) not null,
			axles_num int not null,
			tyre_num int not null,
			roadtax_expiry varchar(10) not null,
			manufacture_year varchar(4) not null,
			CONSTRAINT pk_vehicle_id primary key (id)
		);

	```

### Notes:
- Run '.\mvnw clean install' to install necessary package defined in pom.xml
- Run '.\mvnw spring-boot:run' to start the Spring Boot application.
