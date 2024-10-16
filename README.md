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





