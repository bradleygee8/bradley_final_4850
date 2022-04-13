stage('Zip Artifacts') {
            steps {
                sh "zip ${imageName}.zip ${imageName}/*"
                archiveArtifacts artifacts: "${imageName}.zip"
            }
        }
