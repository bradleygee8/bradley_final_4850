//Name: Bradley Gee
//April 13 2022
//Description: Installs the requirements, uses pylint to look for the code quality, runs the scripts and zips all of the files that end in .py
    pipeline{
    agent any
    parameters{
        choice(
        choices: 'run',
        description:'If you have the parameters run  it will run the stage Run Scripts',
        name: 'TARGET')
        }
    stages{
        stage('Build'){
            steps{
                echo "Name: A01031100 Group:21"
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
            when {
                expression{params.TARGET == "run"}
            }
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
