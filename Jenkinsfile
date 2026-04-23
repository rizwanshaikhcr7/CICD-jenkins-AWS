node {
    def appDir = 'var/www/nextjs-app'
    
    stage('Clean Workspace') {
        deleteDir()
    }
    
    stage('Clean repo'){
        echo 'cleaing the repo'
        git(
            branch: 'main',
            url: 'https://github.com/rizwanshaikhcr7/CICD-jenkins-AWS'
        )
    }

    stage('Deploy to ec2')
      echo 'Deploying to EC2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R 
            jenkins:jenkins ${appDir}

            rsync -av --delete
            --exclude= '.git' 
            --exclude= 'node_modules' .
            / ${appDir}

            cd ${appDir} 
            sudo npm install
            sudo npm run build
            sudo fuser -k 3000/tcp ||
            true
            npm start 
        """

}



