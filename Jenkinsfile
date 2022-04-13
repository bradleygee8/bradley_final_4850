//Name: Bradley Gee
//April 13 2022
//Description
def call(TARGET) {
    pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                echo "Running the Requirements"
                sh "pip install -r ./requirements.txt"
                echo "Requirements Complete" 
        }
        }
        stage("Code Quality"){
            steps{
                sh "pylint --fail-under=7.0 ./*.py"
                
        }}
        stage("Code Quantity"){
            steps{
                sh "find . -type f -name '*.py' | xargs wc -l"
            }
        }
        stage("Run Scripts"){
            steps{
                sh "python3 main.py phone text output"
                sh "python3 main.py tablet csv ouput"
                sh "python3 main.py laptop json ouput"
            }
        }
         stage('Zip') {
            steps {
                sh "zip exam.zip ./*.py"
                archiveArtifacts artifacts: "exam.zip"
            }
        }

}

}
}
