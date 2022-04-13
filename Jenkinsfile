//Name: Bradley Gee
//April 13 2022
//Description
    pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                sh "pip install -r ./requirements.txt"
                sh "echo "Requirements Complete" 
        }
        }
        stage("lint"){
            steps{
                sh "pylint --fail-under=7.0 ./*.py"
                //$(find . -name "*.py" | xargs)
        }}
}

}
