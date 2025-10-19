# Dev-- wha?? — The Evolution from SysAdmin to DevOps and Why It Matters

---

## 🌍 Introduction

The term **DevOps** has become one of the most defining concepts in modern IT and software delivery. It represents not just a role or toolset, but a **cultural and technical transformation** that unites software development (**Dev**) and IT operations (**Ops**) into one collaborative process.

Traditionally, developers wrote code and “threw it over the wall” to operations teams, who deployed and maintained it. This led to **slow releases**, **reliability issues**, and **communication silos**. DevOps breaks that wall down.

At its heart, **DevOps is about speed, stability, and collaboration** — helping organizations deliver high-quality software faster, more securely, and with continuous improvement.

---

## 🚀 The DevOps Philosophy

DevOps integrates **people**, **processes**, and **tools** to shorten the development lifecycle. Its goal is to ensure that software evolves **rapidly and reliably**, without compromising stability or user experience.

Here’s how DevOps transforms traditional workflows:

| Traditional Model | DevOps Model |
|--------------------|--------------|
| Developers write code, Ops deploys | Developers and Ops collaborate end-to-end |
| Manual builds and testing | Automated CI/CD pipelines |
| Infrequent releases | Continuous deployment and feedback |
| Reactive troubleshooting | Proactive monitoring and observability |

---

## 🧩 The Core DevOps Lifecycle

DevOps can be visualized as an **infinity loop**, representing continuous processes that feed into each other:

<img width="1361" height="165" alt="image" src="https://github.com/user-attachments/assets/4cdfb30b-36cc-4a10-9478-ac2407a9a2a4" />

Each phase supports automation, collaboration, and feedback:

Plan → Requirements, user stories, backlog management.

Code → Writing modular, testable software.

Build → Automated builds via Jenkins, GitHub Actions, or GitLab CI.

Test → Automated unit, integration, and security testing.

Release/Deploy → CI/CD pipelines for seamless delivery.

Operate/Monitor → Continuous visibility through Prometheus, Grafana, and **ELK**.

🛠️ Key Tools in the DevOps Ecosystem
| Category | Common Tools |	Function |
|-------------------|-------------|----------|
| Version Control |	Git, GitHub, GitLab |	Manage source code collaboratively |
| CI/CD	| Jenkins GitHub Actions, GitLab CI | Automate build, test, and deployment |
| Infrastructure as Code (IaC) | Terraform, Ansible, CloudFormation |	Automate provisioning of infrastructure |
| Containerization	| Docker, Podman |	Package applications and dependencies |
| Orchestration |	Kubernetes, Helm |	Manage containerized workloads |
| Monitoring |	Prometheus, Grafana, Zabbix |	Visualize performance and health |
| Security	| SonarQube, Trivy, Vault |	Integrate security into pipelines (DevSecOps) |

🧱 Architecture of a Typical DevOps Environment
Below is a simplified view of how DevOps integrates across teams and infrastructure layers:

<img width="733" height="834" alt="image" src="https://github.com/user-attachments/assets/3ad24d30-5acb-4494-8a4e-96c155b7b859" />
---------
<img width="276" height="833" alt="image" src="https://github.com/user-attachments/assets/279352f9-2cff-4f6c-831c-5e0a3cc5c49f" />

💻 Hands-On Example — Automating App Setup and Deployment

To make DevOps practical, let’s walk through a short automation exercise where we:
- Set up Node.js and NPM.
- Download and deploy a simple Node.js application from AWS S3.
- Run it in the background.

Below is the annotated Bash script you can execute on an Ubuntu VM.

# EXERCISE: Automate Node.js App Setup and Deployment

#!/bin/bash
#EXERCISE 9: 8-extended Start Node App- 
#Refresh repo index
apt update -y

#Create user environment variable 
NEW_USER=myapp

#Accept input into Log_directory
read -p LOG_DIRECTORY

if [ -d $LOG_DIRECTORY ]
then
    echo "$LOG_DIRECTORY exists"
else
    echo "creating a new directory"
    mkdir -p $LOG_DIRECTORY

#Install NodeJS
apt install -y nodejs

#install NPM
apt install -y npm

#Get versions of NodeJs and NPM and confirm both are installed
nodejs_version=$(nodejs --version)
npm_version=$(npm --version )

if [ -z "$nodejs_version" ] && [ -z "npm_version" ]
then
	echo "Nodejs $nodejs_version and Npm $npm_version installed not present."
else
	echo "Nodejs $nodejs_version and Npm $npm_version present and  installed."
fi

Get artefact from AWS repo
runuser -l $NEW_USER -c "wget https://node-envvars-artifact.s3.eu-west-2.amazonaws.com/bootcamp-node-envvars-project-1.0.0.tgz."

#Unzip the tar file
runuser -l $NEWUSER -c "tar -xvzf bootcamp-node-envvars-project-1.0.0.tgz"

#Set environmental variables
export APP_ENV=dev
export DB_USER=myuser
export DB_PWD=mysecret
source ~/.bashrc

#Change the directory to the directory of the unzipped tar file
cd package/

#Run NodeJS server in background
npm install &
node server.js & 

#Check if node server is running
ps -aux | grep nodejs

#Show port in use
sudo netstat -lntp | grep :3000




`#!/bin/bash`

**Refresh repository index**
`apt update -y`

#Define environment variable
`NEW_USER=myapp`

# Accept input into Log directory

read -p *Enter log directory path: * LOG_DIRECTORY

if [ -d *$LOG_DIRECTORY* ]; then
    echo *$LOG_DIRECTORY exists*
else
    echo *Creating new directory...*
    mkdir -p $LOG_DIRECTORY
fi

**Install NodeJS
apt install -y nodejs

**Install NPM
apt install -y npm

**Verify installation
nodejs_version=$(nodejs --version) npm_version=$(npm --version)

if [ -z *$nodejs_version* ] && [ -z *$npm_version* ]; then
    echo *NodeJS or **NPM** not installed.*
else
    echo "NodeJS $nodejs_version and **NPM** $npm_version installed successfully."
fi

**Get application artifact from AWS repo
runuser -l $NEW_USER -c "wget [https://node-envvars-artifact.s3.eu-west-2.amazonaws.com/bootcamp-node-envvars-project-1.0.0.tgz"](https://node-envvars-artifact.s3.eu-west-2.amazonaws.com/bootcamp-node-envvars-project-1.0.0.tgz*)

**Extract tar file
runuser -l $NEW_USER -c *tar -xvzf bootcamp-node-envvars-project-1.0.0.tgz"

**Set environment variables**
export APP_ENV=dev export DB_USER=myuser export DB_PWD=mysecret source ~/.bashrc

**Navigate to extracted package**
cd package/

**Install dependencies and start app**
npm install & node server.js &

**Check Node process**
ps -aux | grep node

**Display open port**
sudo netstat -lntp | grep :**3000** *

echo *✅ Node app deployed successfully!*
