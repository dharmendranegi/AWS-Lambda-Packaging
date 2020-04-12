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

**NOTE**  Steps 2, 5, 6 and 8 will be not mention here. For these steps you can check my another project : [Getting Started with Git-Lab CI-CD FOR AWS](https://github.com/dharmendranegi/-Python-CI-CD-Tutorial-)
   

**Creating a project with some pyhton functions**

Our file structure for project:

     src
        folder1
            folder1-a
                function4.py
                requirements.txt   # which will include your module names
            function5.py
        folder2
            function3.py
            requirements.txt       # which will include your module names
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
    .gitlab-ci.yml

  
**NOTE** Root requirements.txt file is empty, because if we enter any module name then that module will be deploy with all lambda function, which we don't want.
  

**Package  dependencies with requierd functions.**

Packaging of function1, this function has no third party dependencies required. (similar for function2)

    handler: src/function1.lambda_handler
    package:
      include:
        - src/function1.py
      exclude:
        - requirements.txt
    name: function1
 
Packaging of function3, this function has third party dependencies included.So, **module** will help you to package function3 with required dependencies.
   
    handler: function3.lambda_handler
    module: src/folder2
    package:
      include:
        - src/folder2/function3.py
      exclude:
        - requirements.txt
    name: function3


Packaging of function4, this function has third party dependencies included. Now, module path is changed as per lambda location.

    handler: function4.lambda_handler
    module: src/folder1/folder1-a
    package:
      include:
        - src/folder1/folder1-a/function4.py
      exclude:
        - requirements.txt
    name: function4
 

Packaging of function5, this function has no third party dependencies included. Again, handler path is changed as per lambda location.

    handler: src/folder1/function5.lambda_handler
    package:
      include:
        - src/folder1/function5.py
      exclude:
        - requirements.txt
    name: function5

**Note** Following configuration in serverless.yml file will help to deploy every function independently(can be done on function level).

    package:
      individually: true   # will help to deploy every function independently.
      exclude:              # excluding files which we don't want to include in package, later include in per function level.
        - "./**"
        - node_modules/**
        - requirements.txt


Here, as we can see we have few lambda functions which have **requirements.txt** with in the folder and few are not.
Because those are the function which required extra dependencies.

You can see difference in packaging with single requirements.txt file for all lambda vs separate reuirements.txt file for required function.

     function's with single requirements.txt file in root with requests module
![](https://github.com/dharmendranegi/AWS-Lambda-Packaging/blob/master/img/function_size_req.png)

     function's with requirements.txt file in root with no module. Also separate reuirements.txt file
     for required function with requests module. 
     Here you can see difference in Code size
![](https://github.com/dharmendranegi/AWS-Lambda-Packaging/blob/master/img/function_size_without_req.png)

     function1 with single requirements.txt file in root with requests module
![](https://github.com/dharmendranegi/AWS-Lambda-Packaging/blob/master/img/function1_with_req.png)

     function1 with single requirements.txt file in root without no module
![](https://github.com/dharmendranegi/AWS-Lambda-Packaging/blob/master/img/function1.png)

     function4 with single requirements.txt file in root with requests module
![](https://github.com/dharmendranegi/AWS-Lambda-Packaging/blob/master/img/function4_with_req_in_root.png)

     function4 with requirements.txt file in root with no module. Also separate reuirements.txt file
     for function4 with requests module
![](https://github.com/dharmendranegi/AWS-Lambda-Packaging/blob/master/img/with_req_in_folder.png)



**Deploying your function.**
git push the changes to your GitLab repository and the GitLab build pipeline will automatically deploy your function.

**For deploying lambda function with api in Aws, check the another project here :[](https://github.com/dharmendranegi/-Python-CI-CD-Tutorial-)

**EveryOne Loves Lambda**
**Go Serverless**
