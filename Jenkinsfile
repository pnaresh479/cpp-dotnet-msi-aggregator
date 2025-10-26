pipeline {
    agent { label 'built-in' } // running this job on jenkins controller node 
    stages {
        stage(' Getting dotnet artifact msi isntaller') {
            steps {
                copyArtifacts(
                    projectName: 'dotnet-calculator2-pipeline',
                    selector: lastSuccessful(),
                    filter: '**/*.msi',
                    target: 'aggreagted/msi/dotnet',
                    fingerprintArtifacts: true
                )
            }
        }

        stage( 'Getting cpp artifact msi installer') {
            steps {
                copyArtifacts(
                    projectName: 'CMakeProject1-pipeline',
                    selector: lastSuccessful(),
                    filter: '**/*.msi',
                    target: 'aggreagted/msi/cpp',
                    fingerprintArtifacts: true
                )
            }
        }

        stage(' verification of artifacts') {
            steps {
                bat 'dir aggreagted\\msi\\dotnet'
                bat 'dir aggreagted\\msi\\cpp'

            }
        }

        stage('Archive aggregated artifacts') {
            steps {
                archiveArtifacts 'aggreagted/msi/**/*.msi', fingerprint: true
            }
        }

    }
}