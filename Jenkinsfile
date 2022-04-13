
    pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                sh "pip install -r ${imageName}/requirements.txt"
        }
        }
        stage("lint"){
            steps{
                sh "pylint --fail-under=5.0 ${imageName}/*.py"
                //$(find . -name "*.py" | xargs)
        }}
        stage("Package"){
            when { 
                expression { env.GIT_BRANCH == 'origin/main' } 
        } 
            steps { 
                withCredentials([string(credentialsId: 'Dockerhub-bradley', variable: 'TOKEN')]) { 
                sh "docker login -u 'bradleygee8' -p '$TOKEN' docker.io" 
                sh "docker build -t ${dockerRepoName}:latest --tag bradleygee8/${dockerRepoName}:${imageName} ${imageName}/." 
                sh "docker push bradleygee8/${dockerRepoName}:${imageName}" 
            } 
        

        }
    }        
        stage('Zip Artifacts') {
            steps {
                sh "zip ${imageName}.zip ${imageName}/*"
                archiveArtifacts artifacts: "${imageName}.zip"
            }
        }
        stage('Deploy') {
            steps {
                sshagent(credentials : ['bradley_acit3855_key']) {
                    withCredentials([string(credentialsId: 'Dockerhub-bradley', variable: 'TOKEN')]) { 
                        sh "ssh -t azureuser@acit3855-bradley.eastus.cloudapp.azure.com -o StrictHostKeyChecking=no 'cd acit4850 && docker-compose pull && docker-compose up -d && exit'"
                    }
                }
            }
}
}

}
