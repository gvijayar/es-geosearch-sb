# SpringBoot and Elastic Search Example on Cloud Foundry

This is a sample SpringBoot application that performs Geo Bounded queries against an Elastic Search instance and plots the data on a map interactively. This application can be run on a workstation or in a cloud environment such as Cloud Foundry. In this example, I will show how to deploy the application on a running Cloud Foundry instance. 

Please follow these steps to deploy this application.

1. Build the project locally
<ul><pre>mvn clean package</pre></ul>

2. Now install the application template in the project namespace. This template includes the environment specific database connection details which will be collected at runtime and subsequently used to build the runtime configuration.
<ul><pre>oc create -f https://raw.githubusercontent.com/gvijayar/jpetstore-tomcat/master/jpetstore-ose3-externaldb.json</pre></ul>

3. Create the application by passing in the necessary database connection information as environment variables. These variables will be used by the S2I process to dynamically build the configuration from the Tomcat pod to connect to the external database.
<ul><pre>oc new-app jws3-tomcat8-postgresql-custom-s2i 
-p DB_HOST=[DATABASE_HOST],DB_PORT=[DATABASE_PORT],DB_DATABASE=[DATABSE_NAME],DB_USERNAME=[USERNAME],DB_PASSWORD=[PASSWORD]</pre></ul>

This application has also been setup to automatically initialize and configure the Postgres database on load - so no additonal database configuration is necessary.

