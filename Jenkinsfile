pipeline{
    agent any
    parameters{
        string(name: 'FILE_NAME', defaultValue: 'app', description: '��� ������������ �����')
        booleanParam(name: 'RUN_UNIT', defaultValue: true, description: '��������� unit �����')
        booleanParam(name: 'RUN_INTEGRATION', defaultValue: true, description: '��������� integration �����')
    }
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
                sh """g++ app.cpp -o ${params.FILE_NAME}"""
            }
        }
        stage('Run Unit Tests'){        
            when{
                expression { return params.RUN_UNIT }
            }
            steps{
                sh """
                   chmod u+x unit_tests.sh
                   ./unit_tests.sh
                   """
            }
        }
        stage('Run Integration Tests'){        
            when{
                expression { return params.RUN_INTEGRATION }
            }
            steps{
                sh """
                   chmod u+x integration_tests.sh
                   ./integration_tests.sh
                   """
            }
        }
        stage('Application Launch Test'){
            steps{
                sh """./${params.FILE_NAME}"""
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