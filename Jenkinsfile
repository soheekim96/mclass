pipeline{
    agent any //어떤 실행 서버에서든 실행 가능

    tools {
        maven 'maven 3.9.11' //Jenkins 에 등록된 Maven 3.9.11을 사용
    }


    environment {
        //배포에 필요한 변수 설정
        DOCKER_IMAGE = "demo-app" //도커이미지이름
        CONTAINER_NAME = "springboot-container" //도커 컨테이너 이름
        JAR_FILE_NAME = "app.jar" //복사할 JAR 파일 이름
        PORT = "8081" // 컨테이너와 연결할 포트

        REMOTE_USER = "ec2-user" //원격 spring 서버 사용자
        REMOTE_HOST = "15.165.230.46" //원격 spring 서버 IP (Public IP)

        REMOTE_DIR = "/home/ec2-user/deploy" //원격 서버에 파일 복사할 경로
        SSH_CREDENTIALS_ID = "30a94d48-312d-4861-a1a0-4de8c1073dfd" // jenkins ssh 자격 증명 IP
    }
        //단계별로 실행될 코드 작성
        stages {
            stage('Git Checkout') {
                steps { //실행될 실제 명령어 작성
                    checkout scm
                    //Jenkins가 연결된 git 저장소에서 최신 코드 체크아웃
                    //SCM(Source Code Management)
                }
            }

            stage('Maven Build'){
                steps {
                    //테스트는 건너뛰고 Maven 빌드
                    sh 'mvn clean package -DskipTests'
                }
            }

            stage('Prepare Jar'){
                steps {
                    //빌드 결과물 jar 파일을 지정한 이름 app.jar로 복사
                    sh 'cp target/demo-0.0.1-SNAPSHOT.jar ${JAR_FILE_NAME}'
                }
            }

        }

    

}