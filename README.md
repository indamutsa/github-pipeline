# Deploying EKS cluster using GITHUB Actions

1. Let us get a working container: \
```
docker rm -f cloud-playgrounqd
docker run -it --rm --name cloud-playgrounqd -v ${PWD}:/root/work -w /root/work --entrypoint /bin/zsh indamutsa/cloud-playground
```

The above container has been already initialized with essentaials kubernetes utilities. \
`eksctl` is already configured.

2. Run this command to initialize the cluster using eksctl

`eksctl create cluster --name arsenelearning --region us-east-1 --nodegroup-name linux-nodes --node-type t2.micro --nodes 2`

 --- Youcan free the resources: \
 ```
 eksctl delete cluster --name arsenelearning --region us-east-1
 ```

3. Create a repository, not in the container but in the host machine. Git is not isntalled on the container since there is no need. Follow the commands below:

```
gh repo create
# You can delete repository this way
------------------------------------
gh repo delete jenkins-pipe --yes
# Follow the instructions
------------------------------------
git status
git add .
git status
git commit -m "First commit"
git push --set-upstream origin master
git status


To  see the current repository: \
--------------------------------
git remove -v
```

2. Then create .github folder and then create workflow folder inside .github folder 

3. create file with .yml extension and write the workflow code

4. Create a github repository 

5. Create secrets in github repo
```
        Go to settings of repo
        click on secrets and variables
```
7. Create ECR, elastic container registry. Once created copy it in the deployment yaml to make sure kubernetes knows where to pull image from.


You can login in ECR in terminal using this command: \
```
docker login -u AWS -p <password> <aws_account_id>.dkr.ecr.<region>.amazonaws.com
```

For instance,
Retrieve an authentication token and authenticate your Docker client to your registry.
Use the AWS CLI:

`aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 274576527624.dkr.ecr.us-east-1.amazonaws.com`

Note: If you receive an error using the AWS CLI, make sure that you have the latest version of the AWS CLI and Docker installed.
Build your Docker image using the following command. For information on building a Docker file from scratch see the instructions here . You can skip this step if your image is already built:

`docker build -t arsenelearning .`


After the build completes, tag your image so you can push the image to this repository:

`docker tag arsenelearning:latest 274576527624.dkr.ecr.us-east-1.amazonaws.com/arsenelearning:latest`

Run the following command to push this image to your newly created AWS repository:

`docker push 274576527624.dkr.ecr.us-east-1.amazonaws.com/arsenelearning:latest`

6. Test application by getting the dns name and going to a web browser


Clean up: Run: eksctl delete cluster --name arsenelearning
