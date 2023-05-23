pipeline {
    agent any
    environment {
        bundle_name = "${bat(returnStdout: true, script: 'echo "FECHA"').trim()}"
    }
    stages {
        stage('PREPARE'){
            steps {
                //bat 'echo ${"Hello world!!"}'
                bat 'echo ${bundle_name}'
                //git credentialsId: "git_hub_ssh", url: "git@github.com:fsergot/dss_pipeline.git"
                //git branch:"origin/main", credentialsId: "hightek2099g", url: "https://github.com/hightek2099g/dss_pipeline.git"
                //bat """sed -i 's|@DESIGN_URAUTO_PROD_URLL@|${https://api-23185367-6220f0a2-dku.us-east-1.app.dataiku.io}|' requirements.txt"""
                //bat "cat requirements.txt"
                //bat "printenv"
            }
        }
        stage('PROJECT_VALIDATION') {
            steps {
                withPythonEnv('python3') {
                    bat "pip install -U pip"
                    bat "pip install -r requirements.txt"
                    bat """pytest -s 1_project_validation/run_test.py -o junit_family=xunit1 --host='${https://api-23185367-6220f0a2-dku.us-east-1.app.dataiku.io}' --api='${W4p8eyvLPkZql7zP51xz4eQcUcaOL4Sv}' --project='${DKU_CHURN}' --junitxml=reports/PROJECT_VALIDATION.xml"""
                }
            }
        }
    }
}
