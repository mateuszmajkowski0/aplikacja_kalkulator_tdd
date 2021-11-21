pipeline {
    agent any
    parameters {
    	gitParameter branchFilter: 'origin/(.*)', defaultValue: 'main', name: 'BRANCH', type: 'PT_BRANCH'
    }
    stages{
        stage('CHECKOUT') {
            steps {
                    checkout([$class: 'GitSCM', branches: [[name: '$BRANCH']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mateuszmajkowski0/aplikacja_kalkulator_tdd']]])
            }
        } // END OF STAGE CHECKOUT
        stage('PYLINT') {
            steps {
                script {
                sh 'python3 -m pylint test_*.py'
                    echo 'wybierz metode'
                }
            }
        } //END OF STAGE PYLINT
        stage('PYTEST') {
            steps {
                script {
                sh 'python3.8 -m pytest test_*.py --html=report.html'
                }
            }
        } //END OF STAGE PYLINT
        stage('CLEANUP') {
            steps {
                script {
                    error 'nie dziala'
                    archiveArtifacts artifacts: 'report.html, assets/', followSymlinks: false
                    deleteDir()
                    
                }
            }
        } // END OF STAGE CLEANUP
    } 
}
