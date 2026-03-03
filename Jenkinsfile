node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace') {
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo') {
        echo 'Cloning the repo'
        git(
            branch: 'main',
            url: 'https://github.com/shubham-pandey1/Jenkins-CI-CD-AWS-Webhosting.git'
        )
    }

    stage('Deploy to EC2') {
    echo 'Deploying to EC2'
    sh """
        mkdir -p ${appDir}
        rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

        cd ${appDir}

        npm install
        npm run build

        fuser -k 3000/tcp || true
        nohup npm run start > app.log 2>&1 &
    """
}
}