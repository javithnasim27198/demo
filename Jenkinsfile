pipeline{
    agent{
        label 'dotprdwcsjnks01'
    }
    options { skipDefaultCheckout() }
    stages{
        stage('checkout-repo'){
            steps{
                cleanWs()
                sh 'echo $USER'
                
                withCredentials([usernamePassword(credentialsId: 'javithpatjenkins', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    script {
                        env.encodedPass=URLEncoder.encode(PASS, "UTF-8")
                    }
                    checkout scm
                    sh '''
                #!/bin/bash
                echo "hello world"
                echo "checking git version"
                git --version
                git branch
                git checkout -b $branch_name
                git push -u origin $branch_name
                '''
}
                
            }
        }
    }
    post {
        // Clean after build
        always {
            cleanWs(cleanWhenNotBuilt: false,
                    deleteDirs: true,
                    disableDeferredWipeout: true,
                    notFailBuild: true,
                    patterns: [[pattern: '.gitignore', type: 'INCLUDE'],
                               [pattern: '.propsfile', type: 'EXCLUDE']])
        }
    }
}
