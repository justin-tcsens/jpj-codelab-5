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

- Add database connection configuration into **application.properties** file, to enable Spring Boot application establish connection over it.
  Verify the database connnection url are matched to your local environment setup.

	```
	spring.application.name=vehicle-management
	server.port=8080

	# JDBC Data Source
	spring.datasource.driverClassName=org.mariadb.jdbc.Driver
	spring.datasource.url=jdbc:mariadb://localhost:3306/jpj-training
	spring.datasource.username=app
	spring.datasource.password=password
	spring.datasource.testOnBorrow=true
	spring.datasource.testWhileIdle=true
	spring.datasource.timeBetweenEvictionRunsMillis=60000
	spring.datasource.minEvictableIdleTimeMillis=30000
	spring.datasource.validationQuery=SELECT 1
	spring.datasource.max-active=15
	spring.datasource.max-idle=10
	spring.datasource.max-wait=8000
	```

- Save application.properties file.
- Open pom.xml file from the project directory.
- Uncomment both JooQ and MariaDB driver dependencies, to enable maven loaded necessary dependencies for compilation, as per following:-
	```
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-jooq</artifactId>
		</dependency>

		<dependency>
			<groupId>org.mariadb.jdbc</groupId>
			<artifactId>mariadb-java-client</artifactId>
			<scope>runtime</scope>
		</dependency>
	```

- Add Maven Flyway plugin execution goal to pom.xml, at the very first entry in <plugins> collection.
  Verify the database connnection url are matched to your local environment setup.
	```
	<!-- Flyway Core -->
		<plugin>
			<groupId>org.flywaydb</groupId>
			<artifactId>flyway-maven-plugin</artifactId>
			<version>8.1.0</version>
			<executions>
				<execution>
					<phase>generate-sources</phase>
					<goals>
						<goal>migrate</goal>
					</goals>
					<configuration>
						<driver>org.mariadb.jdbc.Driver</driver>
						<url>jdbc:mariadb://localhost:3306/jpj-training</url>
						<user>app</user>
						<password>password</password>
					</configuration>
				</execution>
			</executions>
		</plugin>
	```

### Notes:
- Run '.\mvnw clean install' to install necessary package defined in pom.xml
- Run '.\mvnw spring-boot:run' to start the Spring Boot application.
