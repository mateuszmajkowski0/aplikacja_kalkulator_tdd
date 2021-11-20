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
                }
            }
        } //END OF STAGE PYLINT
        stage('PYTEST') {
            steps {
                script {
                sh 'python3 -m pytest test_*.py'
                }
            }
        } //END OF STAGE PYLINT
        stage('CLEANUP') {
            steps {
                script {
                    archiveArtifacts artifacts: 'report.html, assets/', followSymlinks: false
                    deleteDir()
                    
                }
            }
        } // END OF STAGE CLEANUP
    } 
}
