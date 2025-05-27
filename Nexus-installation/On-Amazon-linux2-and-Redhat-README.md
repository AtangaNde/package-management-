### AWS Acccount.

### Create Redhat EC2 t2.medium Instance with 4GB RAM.

### Create Security Group and open Required ports. 8081

### Attach Security Group to EC2 Instance.

### Install java openJDK 1.8+ for Nexus version 3.15


      #!/bin/bash
      sudo hostnamectl set-hostname nexus
      sudo useradd nexus
      sudo echo "nexus ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/nexu
      cd /opt
      sudo yum install wget git nano unzip -y
      sudo yum install java-11-openjdk-devel java-1.8.0-openjdk-devel -y
      sudo wget http://download.sonatype.com/nexus/3/nexus-3.15.2-01-unix.tar.gz 
      sudo tar -zxvf nexus-3.15.2-01-unix.tar.gz
      sudo mv /opt/nexus-3.15.2-01 /opt/nexus
      sudo rm -rf nexus-3.15.2-01-unix.tar.gz
      sudo chown -R nexus:nexus /opt/nexus
      sudo chown -R nexus:nexus /opt/sonatype-work
      sudo chmod -R 775 /opt/nexus
      sudo chmod -R 775 /opt/sonatype-work
      /bin/bash

### run the below command to add nexus as a user in nexus

      echo  'run_as_user="nexus" ' > /opt/nexus/bin/nexus.rc

### create soft link for nexus

     sudo ln -s /opt/nexus/bin/nexus /etc/init.d/nexus

## Start nexus

      sudo systemctl enable nexus
      sudo systemctl start nexus
      sudo systemctl status nexus


## The below script will automate the process

      #!/bin/bash
      sudo hostnamectl set-hostname nexus
      sudo useradd nexus
      sudo echo "nexus ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/nexus
      cd /opt
      sudo yum install wget git nano unzip -y
      sudo yum install java-11-openjdk-devel java-1.8.0-openjdk-devel -y
      sudo wget http://download.sonatype.com/nexus/3/nexus-3.15.2-01-unix.tar.gz 
      sudo tar -zxvf nexus-3.15.2-01-unix.tar.gz
      sudo mv /opt/nexus-3.15.2-01 /opt/nexus
      sudo rm -rf nexus-3.15.2-01-unix.tar.gz
      sudo chown -R nexus:nexus /opt/nexus
      sudo chown -R nexus:nexus /opt/sonatype-work
      sudo chmod -R 775 /opt/nexus
      sudo chmod -R 775 /opt/sonatype-work
      sudo echo  'run_as_user="nexus" ' > /opt/nexus/bin/nexus.rc
      sudo ln -s /opt/nexus/bin/nexus /etc/init.d/nexus
      sudo su - nexus -c "/opt/nexus/bin/nexus enable"
      sudo su - nexus -c "/opt/nexus/bin/nexus start"
      sudo su - nexus -c "/opt/nexus/bin/nexus status"




## Troubleshooting

nexus service is not starting?

a)make sure  to change the ownership and group to /opt/nexus and /opt/sonatype-work directories and permissions (775) for nexus user.

b)make sure you are trying to start nexus service AS nexus user.

c)check java is installed or not using java -version command.

d) check the nexus.log file which is availabe in  /opt/sonatype-work/nexus3/log  directory.

## Unable to access nexus URL?

a)make sure port 8081 is opened in security groups in AWS ec2 instance.
