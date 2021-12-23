# DevOps
This respository is basically for all the DevOps technologies

# Create a Jenkins VM using the Template.
1. Open the inbound port 8080 as Jenkins listens on 8080 port.
2. Check if java installed "java -version", if not then install using "yum install java-1.8*" command.
    Get the java location using "$(dirname $(dirname $(readlink -f $(which javac))))" command.
    Add java path "PATH=$PATH:$HOME/bin:$JAVA_HOME" to .bash_profile.
    Run "echo $JAVA_HOME" to verify the java path.
3. To download and install jenkins for CentOS follow the commands on https://pkg.jenkins.io/redhat-stable/ 
4. systemctl status jenkins
    systemctl start jenkins
    systemctl enable jenkins
5. Run below command to get the initialAdminPassword.
    # cat /var/lib/jenkins/secrets/initialAdminPassword
6. Open <Jenkins-public-IP>:8080 in the browser. Copy the password from step 5 and paste in browser window to login to jenkins.
   Select Customize jenkins (Install suggested plugins OR Select Plugins to Install). We can skip this and start using jenkins directly.
