pipeline {
    agent {
        // Provisions a fresh Pod per build by inheriting the "maven"
        // podTemplate registered under jenkins.clouds in casc.yaml (in the
        // devsecops-stack repo), instead of running the build inside the
        // Jenkins controller container. That image already has Maven on
        // PATH, so no `tools { maven ... }` needed. `inheritFrom` (not
        // `label`) is what actually picks up the cloud-defined template by
        // name; `label` alone only names a new, empty inline template and
        // is deprecated for this purpose.
        kubernetes {
            inheritFrom 'maven'
            defaultContainer 'maven'
        }
    }
    stages {
        // No explicit checkout stage: this job is configured as "Pipeline
        // script from SCM" pointing at this repo, so Jenkins already checks
        // it out into the workspace before running any stage.
        stage('Build, Test & Analyze') {
            steps {
                dir('demo') {
                    withSonarQubeEnv('SonarQube') {
                        sh 'mvn clean verify sonar:sonar -U'
                    }
                }
            }
            post {
                always {
                    junit 'demo/target/surefire-reports/**/*.xml'
                }
            }
        }

        // stage('Publish Artifact') {
        //     steps {
        //         sh 'cd demo && mvn deploy'
        //     }
        // }
    }
}
