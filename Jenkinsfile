pipeline {
    agent any

    environment {
        wokerUrl = "www.baidu.com"
    }

    stages {
        stage('拉取/更新代码') {
            steps {
                echo "拉取/更新代码"
            }
        }

        stage('构建/打包项目') {
            steps {
               echo "构建/打包项目"
               sh "source /etc/profile && gitbook install && gitbook build"
            }
        }

        stage('发布项目') {
          steps {
             echo "发布项目"
             sh "tar -cvzf ROOT-saas-plus-gitbook.tar.gz _book/ --exclude=_book/.* --exclude=_book/Jenkinsfile"
             sh "scp -o StrictHostKeyChecking=no ROOT-saas-plus-gitbook.tar.gz worker1:/root/"
          }
        }

        stage('检查是否正常部署') {
            steps {
                script {
                  def exitValue = sh(script: "curl ${wokerUrl}", returnStatus: true)
                  echo "return exitValue :${exitValue}"
                  if(exitValue != 0){
                      echo "无法访问"
                      sh 'exit 1'
                  }
                }
            }
        }
    }
}
