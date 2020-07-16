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
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                script {//填写运行代码
                    tools.PrintMes("xu happy", "red")
                }
            }
        }
    }
}
