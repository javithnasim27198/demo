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
                checkout scm
                withCredentials([usernamePassword(credentialsId: 'javithpatjenkins', passwordVariable: 'pass', usernameVariable: 'user')]) {
    // the code here can access $pass and $user
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
