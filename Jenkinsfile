#!groovy

@Library('jenkinslib') _

def tools = new org.devops.tools()

String workspace = "/opt/jenkins/workspace"

pipeline {

    agent {
        node {  
            label "master"   //指定运行节点的标签或者名称
            customWorkspace "${workspace}"   //指定运行工作目录（可选）
        }
    }
    parameters { string(name: 'test', defaultValue: 'staging', description: '') }
   
    options {
        timestamps()  //日志会有时间
        skipDefaultCheckout()  //删除隐式checkout scm语句
        disableConcurrentBuilds() //禁止并行
        timeout(time: 1, unit: 'HOURS')  //流水线超时设置1h
    }
    
    stages {
        stage('Hello') {
//            when { environment name: 'test', value: 'abcd' }
            steps {
                echo 'Hello World'
                script {//填写运行代码
                    tools.PrintMes("xu happy", "red")
//                    emailext body: '1455870304@qq.com', subject: '1455870304@qq.com', to: '1455870304@qq.com'
//                    input id: 'Test', message: '我们是否要继续？', ok: '是，继续吧！', parameters: [choice(choices: ['a', 'b'], description: '', name: 'test1')], submitter: 'lizeyang,admin'
                }
            }
        }
         //下载代码
        stage('GetCode'){ //阶段名称
            steps{
                 script{ //填写运行代码
                        tools.PrintMes("获取代码",'green')
                        println("${test}")
                }
            }
        }
        stage("mavenBuild"){
            steps{
                script{
                    tools.PrintMes("开始Build代码",'green')
                    def mvnName = tool 'maven3'
                    sh "source /etc/profile"
                    sh "${mvnName}/bin/mvn clean package"
                }
            }
        }
    }
    
    post {
        always {
            script{
                println("always")
            }
        }

        success {
            script{
                currentBuild.description = "\n 构建成功!" 
            }
        }

        failure {
            script{
                currentBuild.description = "\n 构建失败!" 
            }
        }

        aborted {
            script{
                currentBuild.description = "\n 构建取消!" 
            }
        }
    }
}
