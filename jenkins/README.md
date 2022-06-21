# jenkins

source: https://dev.to/andresfmoya/install-jenkins-using-docker-compose-4cab

## Step
1. Run the server `docker-compose up -d`
2. Check docker log `docker logs jenkins | less`
3. Get initial password `docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword`
4. Open http://localhost:8081/

username: admin
password: [get from initial password]

## Setup Plugin Golang
Tutorial: https://www.youtube.com/watch?v=U8hg9nBieqw

Install Plugin Pipeline Step: (https://plugins.jenkins.io/workflow-aggregator/)
1. go to `Manage Jenkins`
2. go to `Manage Plugin`
3. choose tab `Available`
4. search `workflow-aggregator`

Install Plugin Go Step: (https://plugins.jenkins.io/golang/)
1. go to `Manage Jenkins`
2. go to `Manage Plugin`
3. choose tab `Available`
4. search `golang`
5. check on the checkbox
6. hit button `Download now and install after restart`
7. hit button `Restart Jenkins when installation is complete and no jobs are running`

Setup Plugin Go Step:
1. go to `Manage Jenkins`
2. go to `Global Tool Configuration`
3. go to `Go` section and hit button `Add Go`
4. fill the name with version golang, example: `1.18.3`
5. click on `Save` button

Create Test job:
1. go to `New Item`
2. fill the name `test-go`
3. choose `Pipeline`
4. Then insert this pipeline script:
```
pipeline {
    agent any

    tools {
        go '1.18.3'
    }
    stages {
        stage('Example') {
            steps {
                sh 'go version'
            }
        }
    }
}

```
5. Save it
6. then click `Build Now`
7. then go to the job. And open `Console Output`

## Setup Credentials Github
1. Go to terminal server jenkins
2. Generate ssh with `ssh-keygen`
3. go to `Manage Jenkins`
4. go to `Manage Credentials`
5. go to `Global credentials`
6. go to `Add Credentials`
7. fill ID: github-kecci
8. fill Desc: Github Kecci
9. fill Username: kecci
10. fill private key: [from ssh id_rsa]

## Advance
if you need administrator for the jenkins, use jenkins-agent, tutorial on: https://www.cloudbees.com/blog/how-to-install-and-run-jenkins-with-docker-compose


Another setup: https://dagshub.com/puneethp/JenkinsDockerSetup
Another tutorial: youtube.com/watch?v=qKI7Y2sUjbU&t=167s