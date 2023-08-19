# AWS-FullDeploymentPiepline

Stages
STAGE 0 : Introduction
STAGE 1 : Create a CodeCommit Repo
STAGE 2 : Configure CodeBuild to clone the repo, create a container image and store on ECR
STAGE 3 : Configure a CodePipeline with commit and build steps to automate build on commit.
STAGE 4 : Create an ECS Cluster, TG's , ALB and configure the code pipeline for deployment to ECS Fargate
STAGE 5 : CLEANUP


STAGE 1 
Create a Code Commit Repo. Configure this Repo and then access this Repo from your local machine.

For Windows Follow : https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-ssh-windows.html
You can download Git from here : https://git-scm.com/download/win
For your refrence Below is how the commands will look like, when  From the emulator you run the ssh-keygen command, and follow the directions to save the file to the .ssh directory for your profile.
<img width="488" alt="image" src="https://github.com/anusachdeva4321/AWS-FullDeploymentPiepline/assets/53436537/6fd183b7-a2e6-4151-b0f9-2f5451b91210">



