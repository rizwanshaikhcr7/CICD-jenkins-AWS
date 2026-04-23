node {
    def appDir = '/var/www/nextjs-app' // Must start with /
    
    stage('Clean Workspace') {
        deleteDir()
    }
    
    stage('Clone Repo') {
        echo 'Cleaning and cloning the repo'
        git(
            branch: 'main',
            url: 'https://github.com/rizwanshaikhcr7/CICD-jenkins-AWS'
        )
    }

    // Added missing curly braces for the stage
    stage('Deploy to EC2') { 
        echo 'Deploying to EC2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            # Fixed rsync formatting to be on a single line or use backslashes
            rsync -av --delete --exclude='.git' --exclude='node_modules' . ${appDir}

            cd ${appDir} 
            npm install
            npm run build
            
            # Kill existing process on port 3000
            sudo fuser -k 3000/tcp || true
            
            # Run in background so Jenkins doesn't hang
            nohup npm start > /dev/null 2>&1 & 
        """
    }
}