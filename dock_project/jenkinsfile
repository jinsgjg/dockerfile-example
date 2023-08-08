pipeline {
     agent any
     triggers {
        githubPush()
    }
    options {
        timestamps()
    }
    stages {
        stage('Github Clone & Checkout') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/jinsgjg/dockerfile-example.git',
                    credentialsId: 'c1973998-0bd2-470d-9f80-31c1a2945b8f'
            }
        }
        stage('nginx Build') {
            steps {
                script {
                    // Docker hub 에 로그인 하기 위해 사용
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                         // Dockerfile로 이미지 생성
                         docker.build('jinsgjg/jenkins-nginx-example', 'dock_project/ubuntu_nginx/nginx/sites-available/default/')
                    }     
                }    
            }
        }
        stage('apache2 Build') {
            steps {
                script {
                    // Docker hub 에 로그인 하기 위해 사용
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                         // Dockerfile로 이미지 생성 
                         docker.build('jinsgjg/jenkins-apache2-example', 'dock_project/ubuntu_apache2/sites-available/000-default.conf/')
                    }     
                }    
            }
        }
        stage('lb Build') {
            steps {
                script {
                    // Docker hub 에 로그인 하기 위해 사용
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                         // Dockerfile로 이미지 생성 
                         docker.build('jinsgjg/jenkins-lb-example', 'dock_project/ubuntu_nginx_loadbalancer/')
                    }     
                }    
            }
        }
        stage('Docker nginx Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        def img = docker.image('jinsgjg/jenkins-nginx-example')
                        img.push('latest')
                        img.push('0.1')
                    }
                }
            }
        }
        stage('Docker apache2 Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        def img = docker.image('jinsgjg/jenkins-apache2-example')
                        img.push('latest')
                        img.push('0.1')
                    }
                }
            }
        }
        stage('Docker lb Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
                        def img = docker.image('jinsgjg/jenkins-lb-example')
                        img.push('latest')
                        img.push('0.1')
                    }
                }
            }
        }
    }
    post {
            cleanup {
                 emailext subject: '$DEFAULT_SUBJECT',
                    to: 'ehdqorwnsdl@gmail.com',
                    body: '$DEFAULT_CONTENT'
            cleanWs() // 작업영역 삭제         
            }
        }
}