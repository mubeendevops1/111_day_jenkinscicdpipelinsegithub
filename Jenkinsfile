node {
    def appDir = '/var/www/nextjs-app'
    def ec2User = 'ubuntu'
    def ec2Host = '3.107.99.15'
    def pemFile = 'D:/DevOpsyoutubeTheTechzeen/workingdirectory/111_day_jenkinscicdpipeline/jenkey.pem'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo'){
        echo 'Cloning the repo'
        git(
            branch: 'main',
            url: 'https://github.com/mubeendevops1/111_day_jenkinscicdpipelinsegithub.git'
        )
    }

    stage('Deploy to EC2'){
        echo 'Deploying to EC2'
        sh """
            rsync -av --delete --exclude='.git' --exclude='node_modules' -e "ssh -i ${pemFile}" ./ ${ec2User}@${ec2Host}:${appDir}

            ssh -i ${pemFile} ${ec2User}@${ec2Host} "
                mkdir -p ${appDir} &&
                cd ${appDir} &&
                npm install &&
                npm run build &&
                fuser -k 3000/tcp || true &&
                nohup npm run start &
            "
        """
    }
}
