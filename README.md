# DevOps
This respository is basically for all the DevOps technologies

# Create a Jenkins VM using the Template.
1. Open the inbound port 8080 as Jenkins listens on 8080 port.
2. Check if java installed "java -version", if not then install using "yum install java-1.8*" command.
    Get the java location using "$(dirname $(dirname $(readlink -f $(which javac))))" command.
    Add JAVA_HOME and java path to .bash_profile.
        JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.el7_9.x86_64
        PATH=$PATH:$HOME/bin:$JAVA_HOME
    Run "echo $JAVA_HOME" to verify the java path.
3. To download and install jenkins for CentOS follow the commands on https://pkg.jenkins.io/redhat-stable/ 
4. Update the hostname  as Jenkins(If not jenkins) by running command "hostname jenkins" then exit and relogin.
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
    Jenkins > New Item > My_First_Jenkins_Job > Build (Add build step as Execute Shell as we are using Linux) > Enter echo "Hello Jenkins" > Apply > Save
    Jenkins > Build Now

# Install GIT on Jenkins Server
    yum install -y git

# Install GIT binaries and dependencies on jenkins
Jenkins > Manage Jenkins > Manage Plugins > Available (search for github) > Select Github and Click on "Install without restart"
    
# Configure GIT for Jenkins
    Jenkins > Manage Jenkins > Global Tool Configuration > Git > Add JDK (Name:git, Path to Git executable=/usr/bin/git) > Apply > Save

# Download and install Maven on Jenkins host
    mkdir -p /opt/maven
    wget https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz
    tar -xzf apache-maven-3.8.4-bin.tar.gz -C /opt/maven
    cd /opt/maven
    mv /opt/maven/apache-maven-3.8.4/* /opt/maven
    
    vi ~/.bash_profile
    M2_HOME=/opt/maven
    M2=/opt/maven/bin
    PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2_HOME:$M2
    
    echo $M2
    echo $M2_HOME
    mvn --version
    
# Install MAVEN binaries and dependencies on jenkins
Jenkins > Manage Jenkins > Manage Plugins > Available (search for maven) > Select Maven Integration, Maven Invoker > Click on "Install without restart"
    
# Configure MAVEN for Jenkins
    Jenkins > Manage Jenkins > Global Tool Configuration > Maven > Add Maven (Name:M2_HOME, MAVEN_HOME=/opt/maven) > Apply > Save
    
Now if we will create a new job in Jenkins, it will show Maven Project as well to choose.
We have build environment for CI/CD pipeline.
   
Using Ansible, we can scrpts in Playbook which will fetch the artifacts and will generate a docker file, push it to docker hub and using that image, it will create a docker container in kubernetes.
