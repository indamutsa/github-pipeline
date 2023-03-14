# Deploying EKS cluster using GITHUB Actions


1. Let us get a working container: \
```
docker rm -f cloud-playgrounqd
docker run -it --rm --name cloud-playgrounqd -v ${PWD}:/root/work -w /root/work --entrypoint /bin/zsh indamutsa/cloud-playground
```

The above container has been already initialized with essentaials kubernetes utilities. \
`eksctl` is already configured.

2. Run this command to initialize the cluster using eksctl

`eksctl create cluster --name arsene_learning --region us-east-2 --nodegroup-name linux-nodes --node-type t2.micro --nodes 2`

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
6. Test application by getting the dns name and going to a web browser


Clean up: Run: eksctl delete cluster --name arsene_learning
