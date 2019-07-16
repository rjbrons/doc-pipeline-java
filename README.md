# doc-pipeline-java

## Deployed Link
- http://deploymentappjava-env.fj3cw39eer.us-west-2.elasticbeanstalk.com/

## Steps
1. Run the app locally and see if there is any error
2. On application properties add -  server.port=5000
3. Update the .gitignore to allow the build folder specifically the application.jar file to not be ignored.
4. Setup the permission to run ./gradlew bootjar by running one of the following commands\
    `chmod +x gradlew` or `chmod 755 gradlew`\
 This will grant the execute permission.\
•	rename the .jar file within build/libs/ to application.jar or\
•	Add this code to your gradle.build before running `./gradlew bootJar`\
`bootJar {
	archiveFileName = 'application.jar'
}`
This specifies the filename to be exactly what is needed for the pipeline without testing / building

![image](https://github.com/rjbrons/doc-pipeline-java/blob/master/asserts/Screen%20Shot%202019-07-16%20at%2011.28.53%20AM.png)

5. Create new application in Elastic Beanstalk <br/>
•	Application name – DeploymentAppJava-env<br/>
•	Platform – Java<br/>
•	Upload your code – upload the jar file<br/>
•	Click create environment<br/>
•	Check the deployed site to see if elastic beanstalk is deployed correctly<br/>

6. Create a pipeline<br> 
![image](https://github.com/rjbrons/doc-pipeline-java/blob/master/asserts/Screen%20Shot%202019-07-16%20at%2011.30.36%20AM.png)
•	Pipeline name – DeploymentAppJava<br/>
•	Select new service role – gives you a role name<br/>
•	Add Source - Select provide – GitHub<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o   Connect to GitHub – Authorize AWS codesuite<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	Should give you a message that you have connected to github<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o	Select the respository<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o	Select the branch<br>
•	Skip the build<br>
•	Add deploy stage<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o	Deploy provider – AWS Elastic Beanstalk<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o	Region – auto populates<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o	Application name – name of your application you have created in elastic beanstalk<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;o	Click next<br>
•	Review your inputs<br>
•	Click create pipeline<br>
•	Make sure you push your code to GitHub with build file in it
![image](https://github.com/rjbrons/doc-pipeline-java/blob/master/asserts/Screen%20Shot%202019-07-16%20at%2012.01.05%20PM.png)

## Potential roadblocks or trouble spots<br> 
•	Deployment issue - Deployment completed, but with errors: During an aborted deployment, some instances may have deployed the new application version. To ensure all instances are running the same version, re-deploy the appropriate application version. Failed to deploy application.<br>
•	Delete the build folder from. gitignore<br>
•	Rename the .jar file to application.jar<br>
•	Push code to master<br>


