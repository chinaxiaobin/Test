@Library('jenkins-share-lib')
def tools = new org.devops.toos()

pipeline {
    agent {
        label "master"
    }
    options {
        timestamps()   //打印步骤执行时间,如果提示timestamps使用问题,可以安装timestamp插件
        timeout(time: 1, unit: 'HOURS')  //timestamps和timeout没有直接联系
    }

    stages {
        stage('GetCode') {
            steps {
                timeout(time:5, unit: 'MINUTES') { //步骤超时时间 
                    script {
                        println('获取代码')
                    }
                }
            }
        }
        stage('Build') {
            steps {
                timeout(time:20, unit: "MINUTES") {
                    script {
                        println{"应用打包"}
                    }
                }
            }

        }
        stage('CodeScan') {
            steps {
                timeout(time: 30, unit: "MINUTES") {
                    script {
                        println("代码扫描")
                        tools.printMes("this is mylib")
                    }
                }
            }
        }
    }
    post {  //和stages对齐
        always {
            script {
                println('always')
            }
        }
        success {
            script {
                currentBuild.description += "\n 构建成功"  //在构建完成后打印描述信息
            }
        }
        failure {
            script {
                currentBuild.description += "\n 构建失败"
            }
        }
        aborted {
            script {
                currentBuild.description += "\n 构建取消"
            }
        }
    }
}


