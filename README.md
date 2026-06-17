This is a demo


Create a maven project (follow the program 2 steps, Get Hello world as output form that Java file)

COMMANDS:

 1)git config --global user.name "tarunpj"

 2)git config --global user.email "tarunprakash.tpj@gmail.com"

 3)git init
 
 4) git add pom.xml

 5) git add src

 6) ssh-keygen -t ed25519 -C "tarunprakash.tpj@gmail.com"

Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/student/.ssh/id_ed25519): 
/home/student/.ssh/id_ed25519 already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase): (just click enter, no need to add any passkey or anything) 
Enter same passphrase again: 
Your identification has been saved in /home/student/.ssh/id_ed25519
Your public key has been saved in /home/student/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:5mk5rgqGzbA6KJl2FH5e9h4Q/dDcA6V49SP4JbtQgno tarunprakash.tpj@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|           ..o   |
|        . = * .  |
|       . = B * + |
|   .    o + + * .|
|. . .  oSE o o   |
| * o . =oo  . .  |
|+o* o o B.   .   |
|Bo o . o o.      |
|+.. ....o.       |
+----[SHA256]-----+



 7)sudo cat /home/student/.ssh/id_ed25519.pub
  you will get ssh keyword , use it in github to create repository(there is an inbuilt option to add that)
  
 8)git commit -m "Integrating Jenkins with Maven"

 9)git remote add origin git@github.com:tarunpj/6thprog_devops(the last part is reposiory name)
  
 10)git config --global push.autoSetupRemote true
 
11)git branch
  
12)git branch -M main
 
13) git branch
 
14) git push origin main(repository created and file uploaded)
  
  
  How to login to Jenkins Dashoboard?
  The jenkin dashboard runs at a local host 8080
  type that in address with user name admin and get password from terminal through the command
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  go back to jenkins dashboard-> go to newitem -> give name -> new pipeline -> paste the script there and click on build 
  
  
  pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sanjayraj45/exampractice.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

    }
}

click save and then click on build now. It will start bulding , then go click on the two options placed under the three dot.




--------------------------------------------------


pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sanjayraj45/exampractice.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
       
        stage("Archive artifacts")
        {
            steps
            {
                archiveArtifacts artifacts: '**/target/*.jar',
                allowEmptyArchive: true
            }
        }
       
        stage("Deploy")
        {
            steps
            {
                sh """
                export ANSIBLE_HOST_KEY_CHECKING=False
                ansible-playbook -i hosts2.ini play3.yml --extra-vars="ansible_become_pass='exam@cse'"
                """
            }
        }

    }
}

after 6th continue:
1) create jar file
gedit first.jar
ls -l first.jar

computer > var > lib > jenkins > workspace > exam..

sudo gedit hosts2.ini > [local] localhost ansible_connection:local
sudo gedit play3.yml (in same terminal of ini)

---
- name: Deploy artifact to localhost
  hosts: localhost
  become: true
  become_method: su

  tasks:
    - name: Copy the artifact to target location
      copy:
        src: /path/to/source/artifact.war
        dest: /path/to/destination/artifact.war


