# AWS-FullDeploymentPiepline

Stages
STAGE 0 : Introduction
STAGE 1 : Create a CodeCommit Repo
STAGE 2 : Configure CodeBuild to clone the repo, create a container image and store on ECR
STAGE 3 : Configure a CodePipeline with commit and build steps to automate build on commit.
STAGE 4 : Create an ECS Cluster, TG's , ALB and configure the code pipeline for deployment to ECS Fargate
STAGE 5 : CLEANUP


STAGE 1 
(1a)Create a Code Commit Repo. 
Configure this Repo and then access this Repo from your local machine.
You can download Git from here : https://git-scm.com/download/win
For Windows Follow : https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-ssh-windows.html
Run cd ~/.ssh
Run ssh-keygen -t rsa -b 4096 and call the key 'codecommit', don't set any password for the key.

Run cat ~/.ssh/codecommit.pub and copy the output onto your clipboard. This is the public part of your key

**P.S :it is important to use ".pub" at end to get the public part of the key.**
In the AWS console move to the IAM console ( https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/home )
Move to Users => Your user name and open that user.
Move to the Security Credentials tab.
<img width="672" alt="image" src="https://github.com/anusachdeva4321/AWS-FullDeploymentPiepline/assets/53436537/ea1c2032-a6d1-43f6-ab06-6f22c035ccf1">

Under the AWS Codecommit section, upload an SSH key & paste in the copy of your clipboard. This is how you interact with code commit. As you give the public SSH key you just generated to aws. You use an SSH key pair.
Copy down the SSH key id into your clipboard

<img width="665" alt="image" src="https://github.com/anusachdeva4321/AWS-FullDeploymentPiepline/assets/53436537/f34b7d49-68da-4cfb-b187-7c3e38d2e459">

Note the Key Id : 
<img width="679" alt="image" src="https://github.com/anusachdeva4321/AWS-FullDeploymentPiepline/assets/53436537/8c8de218-2939-4b63-a9d7-25a36790d025">

From your terminal, run nano ~/config and at the top of the file add the following:

Host git-codecommit.*.amazonaws.com
  User KEY_ID_YOU_COPIED_ABOVE_REPLACEME
  IdentityFile ~/.ssh/codecommit

  Replace KEY_ID_YOU_COPIED_ABOVE_REPLACEME with the SSH KEY ID( **This is not a AWS Sectert Key. This is the key we use everytime we authenticate to aws code commit.**)

 Save the file( Clt + X) and run a chmod 600 ~/.ssh/config to configure permissions correctly.

  <img width="948" alt="image" src="https://github.com/anusachdeva4321/AWS-FullDeploymentPiepline/assets/53436537/e3f0b832-9f52-4190-b810-049d3088b0a3">

(1b)Creating the code commit repo for cat pipeline
Move to the code commit console (https://us-east-1.console.aws.amazon.com/codesuite/codecommit/repositories?region=us-east-1)
Create a repository.
Call it codecommit-XXX where XXX is some unique numbers. I usually prefer to add the date from today.
Once created, locate the connection steps details and click SSH
Locate the instructions for your specific operating system.
<img width="664" alt="image" src="https://github.com/anusachdeva4321/AWS-FullDeploymentPiepline/assets/53436537/3d046e41-088f-4d6a-b2a8-8a7230014bec">

Locate the command for Clone the repository and copy it into your clipboard.
<img width="405" alt="image" src="https://github.com/anusachdeva4321/AWS-FullDeploymentPiepline/assets/53436537/d9c882e6-46d8-4af6-bede-6efaef9817b6">

In your terminal, move to the folder where you want the repo stored. Generally i create a repos folder in my home folder using the mkdir ~/repos command, then move into this folder with cd ~/repos
then run the clone command, which should look something like ssh://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-XXX
You can download https://github.com/anusachdeva4321/AWS-FullDeploymentPiepline/blob/3783ba5b071d870da134dd4ca892a671d3445d5d/Lab_Setup/container.zip








