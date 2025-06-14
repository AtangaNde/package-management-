# SIMPLIFIED STEPS TO FOLLOW WHEN INSTALLING MAVEN

### Login into your AWS account

### Launch an EC2 T2.medium instance with 4GB of RAM

### Create a security group and open port 22

### Attach the security group to the instance

Run the command bellow to change the hostname of your server to maven

           sudo hostnamectl set-hostname maven

Switch to ec2-user so as to enforce your new hostname with the command;

            sudo su - ec2-user

For maven to run, we need some prerequities, and these prerequities are;
java, git, unzip, 

you should note that for maven to run, java must be running,
And do not forget the fact that in Linux, all packages are instaled
or downloaded in the opt directory

so for you to download the prerequities of maven, first move to the opt 
directory by running the command,

              cd /opt

Now that you are in the opt directory, you can install the packages by 
running the command;

              sudo yum install wget vim tree unzip git
              sudo yum install java-11-openjdk-devel

Now that you have installed the prerequities for maven to run, 
you can check if java-11-openjdk-devel is running by running 
the command;
        
            java -version

equally you can check the version of git installed by running
the command;

             git --version

now that you are sure that java is installed, you can now move 
ahead to download the maven software from the internet by running 
the command;

              sudo wget https://dlcdn.apache.org/maven/maven-3/3.9.4/binaries/apache-maven-3.9.4-bin.zip

After you have run this command, check if the maven software was downloaded by
running the command;

                 ls

You will see a downloaded .zip file in a red colouration, 
Extract the .zip file by running the command;

                sudo unzip apache-maven-3.9.4-bin.zip

After running the above command, check if the file has been extracted by running

                  ls

At this point, you will see that we have the .zip file in a red colouration and
the extracted file in blue colouration, since you have two same files, you will no 
more be needing the .zip file, so to delete it, run the command bellow,

                sudo rm -rf apache-maven-3.9.4-bin.zip

Check again to be sure that the .zip file was deleted by running,

                  ls

You will now see that you are having only one file there with a blue colouration,
Rename the file to a more portable name , 
for example , maven -----> by running the command,

                 sudo mv apache-maven-3.9.4/ maven

Now that you have downloaded and extracted maven, you shoud know
that maven has a home directory, and for maven to do a build with the
mvn command, you must define that home directory in the system , For you 
to do that, you will have to vi into the maven configuration file and define 
the path there, run the bellow command to vi into the configuration file;

                 
               vi ~/.bash_profile

Now that you are in the file, enter into insert mode by pressing letter 

            i  on you keyboard

**Copy the below two paths and paste them in between commented lines**  

            export M2_HOME=/opt/maven
            export PATH=$PATH:$M2_HOME/bin

You should be very careful when you are into the file because if you mess
up that file, maven will not be able to do a build

After modifying the file, press the Esc on you keyboard to go out of insert
mode, then :wq! to save and quit

NOTE should be taken that when you modify a file in the system. you have to
notify the system about the change so that the system will re-enforce the
changes, in this case, you will run the bellow command;

               source ~/.bash_profile

When you run this command, the system will re-enforce the changes and you 
can now check if maven is running by ;

                 mvn -version

You will now see the version of maven that you have successfully install.

At this point, you have successfully installed maven and now ready to do 
a build,


For you to do a build, you will now go out of the /opt by running the command

                  cd

With the cd command, you are free to navigate directories, so by running this 
command, you move back to the home of ec2-user,

Now create a project directory by running the command,

                  mkdir java-project

After running the command, check if the directory was created by running the
command,

                  ls

Now that the project directory has been created, switch to it by running the 
 command

                 cd java-project

In this directory, clone you project url by running the command 

        git clone url

Here, the url will be given to you by the company , for example ,you have been 
given the url bellow

                   
        https://github.com/Atangoinfotech/maven-standalone-application

Since for you to do a build, you will have to clone the url, in this exapmle,
you are going clone the above url by running the command 

        git clone https://github.com/Atangoinfotech/maven-standalone-application

After cloning this repository url, check if you have the code (file) that was cloned with 

             ls

Rename the file to a more portable file by running

          sudo mv maven-standalone-application msa

check to see if it was renamed by

              ls

Now that you have msa, switch to msa by running the command

            cd msa

In msa, you can now do a build with maven by running the command

            mvn package


When you run the command mvn package, it will;

       validate the code
       compile the code
       run unit test cases 
and create packages in the target directory in the form of artifacts,

what am trying to tell you here is that, in maven, we have commands like;

       mvn validate -----> this will validates the codes
       mvn compile  -----> this will compile the code
       mvn test     -----> this will run unit test cases on the codes
       mvn package  -----> this will create packages in the target directory in the             
                           form of artifacts 
       mvn intsall  -----> this will create packages in the target directory and in
                           the maven home directory

But here , we will mostly be running the mvn package because, when you run the 
mvn package, it;
         
        validates the codes, compile them , run inut test cases on then and 
        create packages in the target directory in the form of artifacts

What do i mean by artifacts here?
artifacts are extentions that identify the type of java code that developers 
wrotes, that is, either a;

          stand-alone-application which ends with ----> .jar
          web applications which ends with        ----> .war
          enterprise applications which ends with ----> .ear

These are the kind of packages that will be created when you a build with maven
depending on the type of apllication respectively.

So when ever you do a build with maven and see taht a package has been created with such extentions,
you shoulod be able to identify them. 

What i will like you to take note of here if that;

     stand-alone-applications are deployed in the ---->  maven server
     web applications                             ----> tomcat/jboss server
     enterprise                                   ----> jboss servers


So when you run the mvn package;
it will create a package for you in the target directory
if you do

          ls

You will see that a target directory was created after running the mvn package command

switch to the target directory by running the command 

        cd target

do 
        ls

you will see that package has been created there with a .jar extension.
that is the package for you

rename it to app.jar by running
  
             sudo mv [apllication] app,jar

you can now deploy the application by running the command

            java -jar app.jar

At this piont, you have deployed a stand-alone-apllication


# YOU CAN BETTER STILL COPY THE SCRIPT BELLOW AND RUN

### AWS Acccount.

### Create Security Group and open Required ports. 22 

### Create Redhat EC2 T2.medium Instance with 4GB of RAM.

### Attach Security Group to EC2 Instance.

### Install java openJDK 1.8+

## Run the below script

    #!/bin/bash
    sudo hostnamectl set-hostname maven
    cd /opt
    sudo yum install wget nano tree unzip git-all -y
    sudo yum install java-11 -y
    sudo wget https://dlcdn.apache.org/maven/maven-3/3.9.4/binaries/apache-maven-3.9.4-bin.zip
    sudo unzip apache-maven-3.9.4-bin.zip
    sudo rm -rf apache-maven-3.9.4-bin.zip
    sudo mv apache-maven-3.9.4/ maven
    /bin/bash

### vi INTO THE CONFIGURATION FILE AND DEFINE THE MAVEN HOME DIRECTORY

###  MAKE SURE YOU PASTE THE PATH IN BETWEEN TWO COMMENTS

### NOTE: cd out of /opt before doing this

  vi ~/.bash_profile 
  
# and add the lines below

  export M2_HOME=/opt/maven
  export PATH=$PATH:$M2_HOME/bin

### AFTER DOING THAT, RUN THE SOURCE COMMAND BELOW TO RESTART THE FILE

source ~/.bash_profile

### CHECK THE DOWNLOADED VERSIONS OF MAVEN , GIT AND JAVA BY RUNNING;

  mvn -version
  java -version
  git --version

## THIS SCRIPT WILL INSTALL AND CONFIGURE APACHE MAVEN

    #!/bin/bash
    cd /opt
    sudo yum install wget nano tree unzip git-all -y
    sudo yum install java-11-openjdk-devel java-1.8.0-openjdk-devel -y
    sudo wget https://dlcdn.apache.org/maven/maven-3/3.9.4/binaries/apache-maven-3.9.4-bin.zip
    sudo unzip apache-maven-3.9.4-bin.zip
    sudo rm -rf apache-maven-3.9.4-bin.zip
    sudo mv apache-maven-3.9.4/ maven

### make sure you cd out of the /opt directory 

# Run

    echo "export M2_HOME=/opt/maven" >> ~/.bash_profile

# Then

    echo "export PATH=$PATH:$M2_HOME/bin" >> ~/.bash_profile

# Restart the .bash_profile by running the below command

    source ~/.bash_profile

    sudo hostnamectl set-hostname maven

    /bin/bash

check if maven is installed

   if [ -x "$(command -v mvn)" ];
   then
    echo "maven is already installed."
    exit 0
   fi

## Or run 

    mvn --version

## YOU CAN STILL AS WELL CONFIGURE MAVEN AS SUCH

   echo "export M2_HOME=/usr/share/maven" >> ~/.bashrc 
   
   echo "export MAVEN_HOME=/usr/share/maven" >> ~/.bashrc
   
   echo "export PATH=${M2_HOME}/bin:$PATH}" >> ~/.bashrc



## THAT IS;

If you run the script bellow, it will do the same task
and it is a more simplier script to use as user data when
when launching and configuring maven directly on the EC2
console dashboard

    #!/bin/bash
    sudo yum update
    sudo yum install maven -y
    echo "export M2_HOME=/usr/share/maven" >> ~/.bashrc
    echo "export MAVEN_HOME=/usr/share/maven" >> ~/.bashrc
    echo "export PATH=${M2_HOME}/bin:$PATH}" >> ~/.bashrc
    sudo hostnamectl set-hostname maven
    sudo su - ec2-user




