pipeline {
    agent any

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
             sh "ls"
          }
        }
    }
}
