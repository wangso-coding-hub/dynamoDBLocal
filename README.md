
Setup environment to run the visualApp application on AWS EC2:

	1.	Create an AWS EC2 instance and add the IAM role that has administrative privileges.
	2.	SCP Upload the visualAPP.tar application onto EC2 using AWS credentials and EC2 IP address
	3.	SSH into the EC2 instance
	4.	Run the following commands on EC2 instance: 
			a. Unzip application: tar xzvf visualAPP.tar
			b. Install JAVA SDK: look up how to on internet
			c. Install apache maven compiler on Amazon Linux: look up how to on internet
			d. Add both maven compiler and JAVA SDK to your environment path variable (if they are not in there already)
	5. 	Setup DynamoDBLocal following instructions on AWS website: 
			https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.html

Start DynamoDBLocal server:
		java -Djava.library.path=./DynamoDBLocal_lib -jar DynamoDBLocal.jar -sharedDb

Run the visual app with DynamoDBLocal in visualApp root path: 

	1.	type the following (replace ??? with your AWS account accessKeyId and secretKey) each in a separate terminal:

		MAVEN_OPTS="-Daws.accessKeyId=??? -Daws.secretKey=???" mvn compile -PdbWriter exec:java

		MAVEN_OPTS="-Daws.accessKeyId=??? -Daws.secretKey=???" mvn compile -Pwebserver exec:java

		Open web browser: type http://localhost:8080 (if not working, use http://localhost:8080/overview.html)

	2.	To change data rate:
		a. Open visualApp/src/main/java/org/example/basicApp/ddb/DynamoDBWriter.java, 
		b. Go to line 122 and change the value from 1000 to 5000 for 5 sec or 10000 for 10 sec.
		c. Open visualApp/src/main/static-content/wwwroot/overview.js, 
		d. Go to line 278 and change the 1000 to 5000 or 10000 based on step 2.b.

	3.	To change name of DynamoDB:
		a. Edit visualApp/pom.xml (rename the DB table to whatever you want to)

	4.	To change number of users:
		a. Open visualApp/src/main/java/org/example/basicApp/ddb/DynamoDBWriter.java
		b. Go to Line 70 and change numUsers=1 to 5, 10, etc.
