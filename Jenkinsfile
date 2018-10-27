pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout'
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '31a5adcd-f936-4634-be55-b5921313cc3c', url: 'https://github.com/lydialiu199403/ImoocTest.git']]])
            }
        }        
        stage('Build') {
            steps {
                echo 'Building'
                sh 'mvn clean install'   //可以用自己的 mvn clean deploy + 参数替代
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                sh 'mvn clean verify sonar:sonar' //此处可以使用mvn test替代，笔者这步是检测代码的质量同步到自己的代码质量检测平台。
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
                sh 'mvn clean deploy'  //此处调用脚本或者ansible、saltstak，部署到远程
            }
        }
    }
}
