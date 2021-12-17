


pipeline {
    agent any
    stages {
        stage("git"){
            steps{
            
                git branch: 'main', credentialsId: 'TEST', url: 'https://github.com/dhlee011/Gitops_Test.git'
            }
        }
        stage('Building image') {
            steps{
                script{
                    sh '''
                    docker info
                    git clone https://github.com/dhlee011/gitops_test.git
                    docker build https://github.com/dhlee011/gitops_test.git#main:.
                    ls -al
                    pwd
                    git remote remove origin
                    '''
                    app = docker.build("902268280034.dkr.ecr.ap-northeast-2.amazonaws.com/dhlee")
                }
            }
        }
        stage('push image') {
            steps{
                script{
                    docker.withRegistry('https://902268280034.dkr.ecr.ap-northeast-2.amazonaws.com', 'ecr:ap-northeast-2:AWSC') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    
                    }                    
                }
            }
        }
        stage('push image2') {
            steps{
                script{
                    sh "git rm -r --cached ."
                    sh "cd .."
                    sh "rm -rf gitops_test"
                    sh "mkdir ww"
                    sh "cd ww"
                    sh "echo 'zzz' > zzz"
                    sh "git remote -v"
                    
                    git branch: 'main', credentialsId: 'TEST', url: 'https://github.com/dhlee011/k8s-manifest.git'
                    withCredentials([[$class: "UsernamePasswordMultiBinding", credentialsId: "TEST", usernameVariable: "dhlee011", passwordVariable: "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"]]) {                                  
                    sh "git remote update origin --prune"
                    sh "git add ."    
                   
                    sh "git remote show origin"
                    sh "git remote -v"
                    
                    sh "git push https://dhlee011:dltk5maxwell2@@github.com/dhlee011/k8s-manifest.git"
                    }               
                }
            }
        }
    }
}
