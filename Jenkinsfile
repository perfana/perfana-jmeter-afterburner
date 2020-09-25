pipeline {

   agent any

    parameters {
        string(name: 'system_under_test', defaultValue: 'Afterburner', description: 'Name used as System Under Test in Perfana')
        string(name: 'jmeterRepo', defaultValue: 'https://github.com/perfana/perfana-jmeter-afterburner.git', description: 'jmeter git repository')
        string(name: 'jmeterBranch', defaultValue: 'master', description: 'jmeter git repository branch')
        choice(name: 'workload', choices: ['test-type-load', 'test-type-stress', 'test-type-slow-backend'], description: 'Workload profile to use in your jmeter script')
        choice(name: 'testEnvironment', choices: ['test-env-acc', 'test-env-local', 'test-env-kubernetes'], description: 'Workload profile to use in your jmeter script')
        string(name: 'annotations', defaultValue: '', description: 'Add annotations to the test run, these will be displayed in Perfana')

    }

    stages {

        stage('Checkout') {

            steps {

                script {

                    git url: params.jmeterRepo, branch: params.jmeterBranch

                }

            }

        }

        stage('Run performance test') {

            steps {

                script {

                    def testRunId = env.JOB_NAME + "-" + env.BUILD_NUMBER
                    def version = "1.0." + env.BUILD_NUMBER
                    def buildUrl = env.BUILD_URL

                    // ** NOTE: This 'M3' maven tool must be configured
                    // **       in the global configuration.

                    def mvnHome = tool 'M3'

                    sh """
                       ${mvnHome}/bin/mvn clean verify -P${params.testEnvironment},${params.workload} -DtestRunId=${testRunId} -DbuildResultsUrl=${buildUrl} -Dversion=${version} -DsystemUnderTest=${system_under_test} -Dannotations="${params.annotations}"
                    """
                }
            }

        }
    }

}


                         
