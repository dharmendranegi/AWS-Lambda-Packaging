# AWS-Lambda-Packaging

Package your **Complex File Structure** Python project with serverless framwork and deploy on AWS using git-lab CI/CD.
As you can package your project with different ways in serverless framwork, but
here we are going to do it using **INCULDE/EXCLUDE** method.



Pre-request : **AWS account. Git account**.

**Example**: In the following example, you will:
    1.  Package python lambda  with dependencies.
    2.  Deploy project using Git-Lab CI/CD.


    
**Steps**: The example consists of the following steps:
    
   1.  Creating a project with some pyhton functions.
   2.  Creating a Lambda handler function
   3.  Package  dependencies with requierd functions.
   4.  Creating a serverless.yml file.
   5.  Crafting the .gitlab-ci.yml file.
   6.  Setting up your AWS credentials with your GitLab account.
   7.  Deploying your function.
   8.  Testing the deployed function.

**NOTE**  Steps 2, 5, and 6 will be not mention here. For these steps you can check my another project : [Getting Started with Git-Lab CI-CD FOR AWS](https://github.com/dharmendranegi/-Python-CI-CD-Tutorial-)
   

**Creating a project with some pyhton functions**

Basic file structure for any project:
    `src
        folder1
            folder1-a
                function4.py
            function5.py
        folder2
            function3.py
        function1.py
        function2.py
    Resources
        function1.yml
        function2.yml
        function3.yml
        function4.yml
        function5.yml
    .gitignore
    requirements.txt
    serverless.yml
    .gitlab-ci.yml`










