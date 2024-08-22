# Agile and DevOps Lab Cheat Sheet
Welcome to the Agile and DevOps Labs
---
## Lab 1: Learning to use Git and its basic operations 

**Objective:**
The objective of this lab is to understand git and github.
•	Creating a remote repository by using GitHub  
•	Downloading the application from the CloudThat AWS S3 bucket
•	Pushing the code into your remote GitHub repository  
•	Branching and Merging

---------------------------------------------------------------------
### Task-1: Creating a Remote Repository Using GitHub

1. Create a **GitHub Account** & **Empty Public Repository** with name as **"hello-world"**

   **Note:** (To SignUp for GitHub Account, [Click Here](https://github.com/signup?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home))

---------------------------------------------------------------------
### Task-2: Download and Install Git Bash

1. Visit the [Click Here](https://git-scm.com/download/win)
2. The website should automatically start downloading the latest version of Git for Windows, which includes Git Bash.
3. Locate the downloaded .exe file and double-click to run the installer.
4. Click 'Install' to start the installation process and wait for it to finish.
5. Find Git Bash in your Start menu or by searching for "Git Bash" in the Windows search bar. Launch it.
```
git --version
```

### Task 3: Initializing the local git repository and committing changes 
```
mkdir lab1 && cd lab1
```
```
curl -O https://hsbctraining.s3.us-east-2.amazonaws.com/hello-world-master.zip
```
```
unzip hello-world-master.zip
```
```
ls
rm hello-world-master.zip
```
```
cd hello-world-master
ls
```
```
git init .
```
To set the `User Identity` ie... `email and user name.` you can use below:

```
git config --global user.email "< Add your email >"
```
```
git config --global user.name "< Add your Name >"
```
```
git status
```
```
git add .
```
```
git status
```
```
git log
```
```
git commit -m "This is the first commit"
```
```
git log
```
```
git status
```

---------------------------------------------------------------------
### Task-4: Pushing the Code to your Remote GitHub Repository  

* Create `Alias` as `Origin` to GitHub's Remote repository URL.
```
git remote add origin < Replace your Repository URL > 
```
(**Example:** `git remote add origin https://github.com/ssamatkar/hello-world.git`)

* To view the list of Aliases, run the below command in Terminal.
```
alias
```
* To view a specific alias use the below command.
```
git remote show origin
```
* Now you can push your code to the Remote repository using the below command.
```
git push origin master 
```

---------------------------------------------------------------------
### Task 5: Creating a Git Branch and Pushing Code to the Remote Repository
* To create a new Branch
```
git branch dev
```
* To know the current branch
```
git branch
```
* To switch to another branch
```
git checkout dev
```
```
git branch
```
```
vi index.html
```
Press INSERT and add the below content
```
<html>
<body>
<h1> Hi There! This file is added in dev branch </h1>
</body>
</html>
```
Save the file using `ESCAPE+:wq!`
```
git status
```
```
git add index.html
```
```
git status
```
```
git commit -m "adding new file index.html in new branch dev"
```
```
git log
```
```
git push origin dev
```
```
git branch
```
```
git branch prod
```
```
git branch
```
```
git checkout prod
```
```
git branch
```
```
git merge dev
```
```
git push origin prod
```
```
git checkout master
```
```
git merge prod
```
```
git push origin master
```

---------------------------------------------------------------------
**Summary:**
1. Initialize a local Git repository on Anchor EC2 instance.
2. Configure Git settings like email and username.
3. Add and commit changes to the Git repository.
4. Create and switch between Git branches.
5. Make changes and commits in different branches.
6. Merge branches and Push the code to a GitHub repository.

#### =============================END of LAB-01=============================
---
## Lab 2: Create a CICD pipeline to auto-fetch the code from GitHub on commits. Build the same using Maven and Deploy it with Tomcat.

**Prerequisites:**
1. JDK

**Objective:**
The objective of this lab is to configure Jenkins to build and deploy applications. It includes `Setting up Jenkins,` `installing necessary plugins` and `configuring Jenkins to build Maven projects,` and `Installing Tomcat Server.` 

### Task 1: Install Jenkins

1.	Download Jenkins MSI Installer: Visit the Jenkins official website and download the Windows installer (jenkins.msi).
2. Run the Installer: Double-click the downloaded jenkins.msi file to start the installation process.
3. Select Installation Options: Choose the installation directory. You can leave the default path or choose a different directory.
4. Service Logon Credentials: By default, Jenkins will run as a Windows service under the Local System account. If you want to run it under a different user account, specify the username and password here.
5. Customize Jenkins Port: By default, Jenkins will use port 8080. If you want to change this port, you can do so during the installation. We will be using port number 8081.
6. Complete the Installation: Once you have configured the options, click Install to start the installation. After the installation is complete, Jenkins will start automatically as a Windows service. You can verify this by looking for Jenkins in services.msc.

### Task 2: Access Jenkins
1.	Open Jenkins in a Browser: Open your web browser and go to
```
http://localhost:8081
```

2. Unlock Jenkins: Jenkins will prompt you to enter an initial admin password.The password is stored in a file on your system. The installer will show you the path to this file, typically something like:
C:\ProgramData\Jenkins\.jenkins\secrets\initialAdminPassword (or) C:\Program Files (x86)\Jenkins\secrets\initialAdminPassword
3. Under Unlock Jenkins, enter the above **initialAdminPassword** & click **Continue**.
4. Click on **Install suggested Plugins** on the Customize Jenkins page.
5. Once the plugins are installed, it gives you the page where you can create a New **Admin User**. 
6. Enter the **User Id** and **Password** followed by **Name and E-Mail ID** then click on **Save & Continue**.
7. In the next step, on the Instance Configuration Page, verify your **Jenkins Public IP** and **Port Number** then click on **Save and Finish**

#### Now you will be prompted to the Jenkins Home Page

1. Click on **Manage Jenkins** > **Plugins** > **Available Plugins** tab and search for **Maven**.
2. Select the "**Maven Integration**" Plugin and "**Unleash Maven**" Plugin and click **Install** (without restart).
3. Once the installation is completed, click on **Go back to the top page**.
4. On Home Page select **Manage Jenkins** > **Tool**.
5. Inside Tool Configuration, look for **Maven installations**, click **Add Maven**. 
6. Give the **Name as "Maven"**, choose **Version as 3.9.5**, and **Save** the configuration.
7. Now you need to make a project for your application build, that selects **New Item** from the Home Page of Jenkins
8. Enter an item name as **hello-world** and select the project as **Maven Project** and then **click OK.**
   ( You will be prompted to the configure page inside the hello-world project.)
9. Go to the "**Source Code Management**" tab, and select Source Code Management as **Git**, Now you need to provide the GitHub Repository **Master Branch URL** and **GitHub Account Credentials**.
10. In the Credentials field, you have to click **Add** and then click on **Jenkins**.
11. Then you will be prompted to the **Jenkins Credentials Provider** page. Under Add Credentials, you can add your **GitHub Username**, **Password**, and **Description**. Then click on **Add**.
12. After returning to the Source Code Management Page, click on Credentials and Choose your **GitHub Credentials**.
13. Keep all the other values as default and select the "**Build**" Tab and inside Goals and options write "**clean package**" and **save** the configuration.

#### Note: The 'clean package' command clears the target directory, Builds the project, and packages the resulting WAR file into the target directory.

16. Now, you will get back to the Maven project "**hello-world**" and click on "**Build Now**" to build the **.war** file for your application

* You can go to **Workspace** > **dist** folder to see that the **.war** file is created there.
* war file will be created in **/var/lib/jenkins/workspace/hello-world/target/**

---------------------------------------------------------------------
### Task 3: Expose Jenkins to the Internet 
Since your Jenkins server is hosted locally, GitHub needs to be able to reach it over the internet to trigger webhooks. You can achieve this by using a tool like ngrok to expose your local Jenkins server to the internet.

1.	Install ngrok: Download and install ngrok from the official website. [Click here](https://ngrok.com/)
This will require you to sign up to their official website for free.
2. Change the directory to the folder where you have installed ngrok.
3.	Expose Jenkins: Run the following command in your git bash:
```
./ngrok http 8081 --log-stdout
```
4. Copy the URL provided in the output of the above command
   e.g. (http://<ngrok_id>.ngrok-free.app/)
--------------------------------------------------------------------
### Task 4: Configure GitHub Webhooks in Jenkins

1. Go to the Jenkins webpage and choose **Manage Jenkins** > **Plugins**
2. Go to the **Available** Tab, Search for **GitHub Integration**. Select the **GitHub Integration Plugin** and then on **Install** (without restart).
3. Once the installation is complete, click on **Go back to the top page**.
4. In your **hello-world project**, Click on **Configure**.
5. Go to **Build Triggers** and enable the **GitHub hook trigger for GITScm polling**. Then **Save**.
6. Go to your **GitHub website**, and inside the **hello-world** repository > **Settings** > **Webhooks** and Click on the **Add Webhook**.
7. Now fill in the details as below.
#### Payload URL Example: 
* http://<ngrok_id>.ngrok-free.app/github-webhook/
* **Content type:** application/JSON

Then, Click on **Add Webhook**.

---------------------------------------------------------------------
### Task 5: Verifying whether the WebHook is working or not by editing the Source Code

1. Now, Make a minor change and commit in GitHub's **hello-world repository** by editing **hello.txt** file.
2. As the source code gets changed, Jenkins gets triggered by the WebHook and starts building the new source code.
3. Go to Jenkins, and you can see a build is happening automatically.
4. Observe the successful build on the Jenkins page.
-------------------------------------------------------------------
### Task 6: Installing and Configuring Tomcat for Deploying our Application on Jenkins Server

![image](https://github.com/janjiralakirankumar/DevOpsEssentials/assets/137407373/d5dde194-f10d-4b4d-a20c-890e9ca3e392)
Step 1: Download Tomcat
1. Go to the Apache Tomcat website. [Click Here](https://tomcat.apache.org/)
2. Navigate to the "Download" section.[Click Here](https://tomcat.apache.org/download-10.cgi)
3. Download the latest binary distribution (usually a .zip file) for Windows (e.g., apache-tomcat-x.x.x-windows-x64.zip).
4. Extract the Tomcat Archive: Right-click the downloaded .zip file and choose "Extract All..." or use a tool like 7-Zip or WinRAR.
5. Extract it to a location of your choice, e.g., C:\Program Files\Apache\Tomcat.
6. Set Environment Variables: Open Control Panel > System and Security > System > Advanced system settings. Click on Environment Variables.
7. Under System Variables, click New and add:
*Variable Name: CATALINA_HOME
*Variable Value: The path to your Tomcat installation, e.g., C:\Program Files\Apache\Tomcat\apache-tomcat-x.x.x.
Optionally, add CATALINA_HOME\bin to the Path variable if you want to run Tomcat commands from any directory.

Step 2: Start Tomcat
1.	Using Git Bash: Open Git Bash.
2. Navigate to the bin directory of your Tomcat installation:
```
cd /c/Program\ Files/Apache/Tomcat/apache-tomcat-x.x.x/bin
```
3. Start Tomcat by running:
./startup.sh
4. If you encounter issues with ./startup.sh, try using startup.bat from Git Bash by calling it directly: ./startup.bat

Step 3: Access Tomcat
1.	Open a Web Browser:
o	Go to http://localhost:8080. This is the default URL for accessing Tomcat’s homepage.
2.	We need to copy the .war file created in the previous Jenkins build from the Jenkins workspace to tomcat webapps directory to serve the web content
cp -R /c/ProgramData/Jenkins/.jenkins/workspace/hello-world/target/hello-world-war-1.0.0.war /c/Users/user/Downloads/apache-tomcat-10.1.28/webapps


#### =============================END of LAB-02=============================
---
## Important Git Commands

Here are some important Git commands and their brief explanations:

1. **`git init`**
   - Initializes a new Git repository in the current directory.

   ```bash
   git init
   ```

2. **`git clone`**
   - Copies a repository from a remote source (like GitHub) to your local machine.

   ```bash
   git clone <repository_url>
   ```

3. **`git add`**
   - Adds changes in the working directory to the staging area for the next commit.

   ```bash
   git add <file>
   ```

4. **`git commit`**
   - Records changes in the repository with a message describing the changes.

   ```bash
   git commit -m "Your commit message"
   ```

5. **`git status`**
   - Shows the status of changes as untracked, modified, or staged.

   ```bash
   git status
   ```

6. **`git diff`**
   - Shows the differences between the working directory and the latest commit.

   ```bash
   git diff
   ```

7. **`git log`**
   - Displays a log of commits, showing commit messages, authors, dates, and commit hashes.

   ```bash
   git log
   ```

8. **`git branch`**
   - Lists existing branches or creates a new branch.

   ```bash
   git branch          # List branches
   git branch <branch_name>   # Create a new branch
   ```

9. **`git checkout`**
   - Switches to a different branch or restores working files from a specific commit.

   ```bash
   git checkout <branch_name>   # Switch to a branch
   git checkout -b <new_branch>   # Create and switch to a new branch
   ```

10. **`git merge`**
    - Combines changes from different branches.

    ```bash
    git merge <branch_name>
    ```

11. **`git pull`**
    - Fetches changes from a remote repository and integrates them into the current branch.

    ```bash
    git pull origin <branch_name>
    ```

12. **`git push`**
    - Uploads local branch commits to the remote repository.

    ```bash
    git push origin <branch_name>
    ```

13. **`git remote`**
    - Lists remote repositories that are connected to your local repository.

    ```bash
    git remote -v   # Show remote repositories with URLs
    ```

14. **`git fetch`**
    - Downloads changes from a remote repository without merging them into your working branch.

    ```bash
    git fetch origin
    ```

15. **`git reset`**
    - Resets the current branch to a specific commit, optionally preserving changes in the working directory.

    ```bash
    git reset --hard <commit_hash>
    ```

These are just a few fundamental Git commands. There are many more, each serving different purposes in the version control process.

---
## DevOps Tools and Documentation Links:

Certainly! Here are the official websites and documentation links for some popular DevOps tools:

1. **Version Control:**
   - **Git:**
     - Website: [Git](https://git-scm.com/)
     - Documentation: [Git Documentation](https://git-scm.com/doc)

2. **Continuous Integration and Continuous Deployment:**
   - **Jenkins:**
     - Website: [Jenkins](https://www.jenkins.io/)
     - Documentation: [Jenkins Documentation](https://www.jenkins.io/doc/)
   - **Travis CI:**
     - Website: [Travis CI](https://travis-ci.com/)
     - Documentation: [Travis CI Documentation](https://docs.travis-ci.com/)

3. **Configuration Management:**
   - **Ansible:**
     - Website: [Ansible](https://www.ansible.com/)
     - Documentation: [Ansible Documentation](https://docs.ansible.com/)
   - **Puppet:**
     - Website: [Puppet](https://puppet.com/)
     - Documentation: [Puppet Documentation](https://puppet.com/docs/)

4. **Containerization and Orchestration:**
   - **Docker:**
     - Website: [Docker](https://www.docker.com/)
     - Documentation: [Docker Documentation](https://docs.docker.com/)
   - **Kubernetes:**
     - Website: [Kubernetes](https://kubernetes.io/)
     - Documentation: [Kubernetes Documentation](https://kubernetes.io/docs/)

5. **Infrastructure as Code:**
   - **Terraform:**
     - Website: [Terraform](https://www.terraform.io/)
     - Documentation: [Terraform Documentation](https://www.terraform.io/docs/index.html)

6. **Monitoring and Logging:**
   - **Prometheus:**
     - Website: [Prometheus](https://prometheus.io/)
     - Documentation: [Prometheus Documentation](https://prometheus.io/docs/introduction/overview/)
   - **ELK Stack (Elasticsearch, Logstash, Kibana):**
     - Website: [Elastic](https://www.elastic.co/)
     - Documentation: [Elastic Stack Documentation](https://www.elastic.co/guide/index.html)

Always check the official websites for the most up-to-date information and documentation. Additionally, many of these tools may have vibrant communities where you can find additional resources, tutorials, and support.

#### ============================= END OF All LABs =============================
