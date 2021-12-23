# DevOps
This respository is basically for all the DevOps technologies

# Create a Jenkins VM using the Template.
1. Open the inbound port 8080 as Jenkins listens on 8080 port.
2. Check if java installed "java -version", if not then install using "yum install java-1.8*" command.
    Get the java location using "$(dirname $(dirname $(readlink -f $(which javac))))" command.
    Add java path "PATH=$PATH:$HOME/bin:$JAVA_HOME" to .bash_profile.
    Run "echo $JAVA_HOME" to verify the java path.
3. To download and install jenkins for CentOS follow the commands on https://pkg.jenkins.io/redhat-stable/ 
4. Update the hostname as Jenkins by running command "hostname jenkins" then exit and relogin.
5. Start and enable jenkins service.
    systemctl status jenkins
    systemctl start jenkins
    systemctl enable jenkins
5. Run below command to get the initialAdminPassword.
    "cat /var/lib/jenkins/secrets/initialAdminPassword"
7. Open <Jenkins-public-IP>:8080 in the browser. Copy the password from step 5 and paste in browser window to login to jenkins.
    Select Customize jenkins (Install suggested plugins OR Select Plugins to Install). We can skip this and start using jenkins directly.

# Change Jenkins user password
    Go to Admin > Configure > Password

# Configure JAVA for Jenkins
    Jenkins > Manage Jenkins > Global Tool Configuration > JDK > Add JDK (Name:JAVA_HOME, JAVA_HOME=Java location from step 2) > Apply > Save

# Create a new Job and validate Jenkins installation
    Jenkins > New Item > My_First_Jenkins_Job > Build (Add build step as Execute Shell as we are using Linux) > Enter "Hello Jenkins" > Apply > Save
    Jenkins > Build Now

# Install GIT on Jenkins Server
    yum install -y git

# Install GIT binaries and dependencies on jenkins
Jenkins > Manage Jenkins > Manage Plugins > Available (search for github) > Select Github and Click on "Install without restart"
    
# Configure GIT for Jenkins
    Jenkins > Manage Jenkins > Global Tool Configuration > Git > Add JDK (Name:git, Path to Git executable=/usr/bin/git) > Apply > Save
