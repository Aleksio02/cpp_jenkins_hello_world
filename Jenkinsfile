pipeline{
    agent any
    stages{
        stage('Print info'){
	    steps{
                sh 'echo "Branch: $(git rev-parse --abbrev-ref HEAD)"'
                sh 'echo "Hash: $(git rev-parse HEAD)"'
                sh 'echo "g++ version: $(g++ --version)"'
            }
        }    
        stage('Build executable file'){
            steps{
                sh 'g++ main.cpp -o main'
            }
        }
        stage('Application Launch Test'){
            steps{
                sh './main'
            }
        }
    }
    post{
        success{
            echo 'You can go home'
        }
        failure{
            echo 'Sit and work on'
        }
    }
}