# CICD_mvn_java
source code with java maven simple project to be integrated with cicd  
Steps:  
Install vscode in ms store with gmail : https://apps.microsoft.com/detail/xp9khm4bk9fz7q?launch=true&mode=full&hl=en-us&gl=in&ocid=bingwebsearch   
install git : https://git-scm.com/downloads/win . git is installed in C:\Program Files\Git . open git bash in the folder you need to clone.     
Java code with maven build: https://github.com/jabedhasan21/java-hello-world-with-maven
Install JDK 8 :  
    Visit the official Oracle website: [JDK 8 Downloads.](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html)  
    You'll need to create an Oracle account to download JDK 8, as it's in the archive  
    Install  
    Installed in C:\Program Files\Java\jdk1.8.2    
    Set environment  
        Step 1: Right-click on This PC or My Computer and select Properties.    
        Step 2: Click Advanced system settings on the left-hand side.  
        Step 3: In the System Properties window, click on the Environment Variables button.  
        Step 4: Under System variables, scroll down and find the Path variable. Select it and click Edit.  
        Step 5: In the Edit Environment Variable window, click New and add the path to your JDK bin directory. This is usually: C:\Program Files\Java\jdk1.8.x_xxx\bin   
        Step 6: Also, add a new System variable:  
                Variable name: JAVA_HOME C:\Program Files\Java\jdk1.8.x_xxx  
    check with java -version command   
Install maven :  
    https://www.baeldung.com/install-maven-on-windows-linux-mac#installing-maven-on-windows  
    install https://maven.apache.org/download.cgi zip - 3.9.9 now  
    Extract to C:\Program Files\Apache\Maven  
    right click on this pc -> advanced system settings    
    edit path as C:\Program Files\Apache\Maven\apache-maven-3.9.9\bin    
    add M2_HOME and MAVEN_HOME variable with value C:\Program Files\Apache\Maven\apache-maven-3.9.9  


Add src code files in src\main\java\hello folder   
Add pom.xml   
Execute "mvn compile"  to get target folder   
"mvn package" to get war file inside target folder . Phases like validate, compile, test, and package are executed.   
"mnv install" to package and install in local m2 repo. In addition to performing everything mvn package does, mvn install  
  also installs the packaged artifact (e.g., JAR or WAR) into the local Maven repository (usually located at ~/.m2/repository on your system).   

Why is the Reduced pom.xml Generated?   
When creating a shaded JAR, Maven combines the project's code with its dependencies into one executable JAR file, which can be distributed without worrying about external dependency management. However, the original pom.xml still lists all the dependencies that were packaged into the JAR. Including these dependencies in future projects would cause them to be added again, which might result in duplicate classes or conflicts.  


To avoid this, Maven generates a reduced pom.xml, which:  

Excludes the dependencies that were already included (shaded) in the final JAR.  
Retains only the necessary dependencies that are still required by consumers of the shaded JAR.  


git config --global user.email "biswas1396@gmail.com"   
git config --global user.email "biswas1396@gmail.com"    
git add .  
git status   
git commit -m "message"   

## Jenkins setup and pipeline execution

download jenkins: https://www.jenkins.io/download/#downloading-jenkins 2.481  
https://www.jenkins.io/doc/book/installing/windows/    
install in C:\Program Files\Jenkins\  
am running it as local <- no admin username n pwd needed  
install java 17 or 21 as it is n=only supported by jenkins  
https://www.oracle.com/java/technologies/javase/jdk21-archive-downloads.html  
choose .exe  
install finish
find password in C:\Program Files\Jenkins\jenkins.err and paste in jenkins login page in web localhost:8080  

install all plugins  
give jenkins username and pwd with email  
jenkins dashboard appears  

##Setup Jenkins  
add jenkins file with jdk and maven version as named in manage jenkins <-- tools ; with its local javahome and maven home paths  
in plugins check for git and pipeline  
Create a New Pipeline Job:

In Jenkins, click on New Item.  
Choose Pipeline and give it a name (e.g., "Maven Build"). here - githubrepo_pipeline   
Under the Pipeline section, select Pipeline script from SCM.  
Choose Git and enter your GitHub repository URL.  
In the Script Path, set the path to the Jenkinsfile (if it's in the root directory, leave it as Jenkinsfile)  
in Manage Jenkins -> tools  
Add JDK - 
JDK  
Name    
JDK 8  
JAVA_HOME  
C:\Program Files\Java\jdk1.8.0_202  
Add Maven  
Maven  
Name  
Maven 3.9.9  
MAVEN_HOME  
C:\Program Files\Apache\Maven\apache-maven-3.9.9  

Jenkis configure:  
Pipeline  
Definition  
Pipeline script from SCM
SCM    
Git  
Repositories  
Repository URL  
https://github.com/DebaratiBiswas/CICD_mvn_java.git  
Branch Specifier (blank for 'any')    
main   
Script Path    
Jenkinsfile  

##ERROR 1 ##

C:\ProgramData\Jenkins\.jenkins\workspace\CICD_mvn_java_pipeline>C:\Program Files\Apache\Maven\apache-maven-3.9.9\bin\mvn.bat package 
'C:\Program' is not recognized as an internal or external command,
operable program or batch file.   
reason: The issue you're facing occurs because the path to Maven contains spaces (i.e., C:\Program Files\). Windows treats spaces in paths as separators unless the entire path is enclosed in quotes.  
solution: Install the plugin:

Go to Manage Jenkins > Manage Plugins.
In the Available tab, search for "Pipeline Maven Integration Plugin".  
stage('Build') {
    steps {
        withMaven(maven: 'Maven3') {
            bat 'mvn package'
        }  
### Add Webhook for build trigger on github push

Step 1: Install the GitHub Plugin in Jenkins    
Go to Manage Jenkins > Manage Plugins.  
In the Available tab, search for the GitHub Plugin and install it.  
Enable GitHub Webhooks Trigger  
In the Build Triggers section jenkins job config, check the GitHub hook trigger for GITScm polling option.  

Step 3: Set Up a GitHub Webhook  
Go to your GitHub repository:  
Open your repository on GitHub.  
Navigate to Settings > Webhooks.  
Click Add webhook.  
Set up the webhook:  
Payload URL: This should be your Jenkins server's URL followed by /github-webhook/ (for example: http://<your-jenkins-url>/github-webhook/).  
Content type: Set this to application/json.  
Which events would you like to trigger this webhook?: Choose Just the push event.  
Click Add webhook.  

## Error 2 ##
when given local host url in github webhook settings  
Payload URL *  
http://localhost:8080/github-webhook/  
error: is not supported because it isn't reachable over the public Internet (localhost)  
reason: Jenkins instance is running on localhost, which is not publicly accessible from the internet. GitHub's webhooks require a publicly accessible URL to send notifications when a repository event occurs (e.g., a push).  
solution:   

Step 1: Sign Up for an ngrok Account    
Go to ngrok's website: https://ngrok.com/download  

Visit the ngrok signup page.  
Create an Account:  

Sign up for a free account using your email, Google, or GitHub credentials.  
Verify Your Account:  

After signing up, check your email and verify your account using the link provided by ngrok.    
Step 2: Get Your ngrok Authtoken  
Log in to ngrok:  

After verifying your account, log in to the ngrok dashboard.
Find Your Authtoken:

In the dashboard, go to the Getting Started section.  
You will find your unique Authtoken under the "Connect your account" step.  
Step 3: Set Up ngrok with Your Authtoken  
Copy the Authtoken:  
https://dashboard.ngrok.com/get-started/your-authtoken  
Copy the authtoken from the ngrok dashboard.  
Run the ngrok Authtoken Command:  

Open Command Prompt or PowerShell.  
Run the following command to authenticate your ngrok installation:  
bash  
Copy code  
ngrok config add-authtoken <your-authtoken>  
Replace <your-authtoken> with the token you copied from the ngrok dashboard.  
Step 4: Run ngrok Again   
Expose Jenkins on Port 8080:  

After authenticating ngrok, run the command again to expose Jenkins:  
bash  
Copy code  
ngrok http 8080   
Get the Public URL:  

ngrok will now provide a public URL (e.g., http://abcd1234.ngrok.io), which you can use to access Jenkins from the internet.  
Step 5: Update the GitHub Webhook with the New URL  
Go to GitHub Webhook Settings:  

Navigate to your repository’s Settings > Webhooks.  
Update the Payload URL:  

Change the Payload URL to the new public URL provided by ngrok (e.g., http://abcd1234.ngrok.io/github-webhook/).  
Save the changes.

Now, your ngrok setup should be complete and functioning with the authenticated account. Let me know if you encounter any further issues!  

output:  
ngrok                                                                                                    (Ctrl+C to quit)                                                                                                                         Found a bug? Let us know: https://github.com/ngrok/ngrok                                                                                                                                                                                          Session Status                online                                                                                     Account                       Debarati (Plan: Free)                                                                      Version                       3.18.0                                                                                     Region                        India (in)                                                                                 Latency                       29ms                                                                                       Web Interface                 http://127.0.0.1:4040                                                                      Forwarding                    https://51e2-122-172-83-194.ngrok-free.app -> http://localhost:8080                                                                                                                                                 Connections                   ttl     opn     rt1     rt5     p50     p90                                                                              0       0       0.00    0.00    0.00    0.00


So here public url is https://51e2-122-172-83-194.ngrok-free.app  
set in github webhooks payload url as https://51e2-122-172-83-194.ngrok-free.app/github-webhook/ save and test the push triggering jenkins build

