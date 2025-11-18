pipeline {
    agent any
    tools{
        jdk 'JAVA_HOME'
        maven 'MAVEN_HOME'
    }
    stages {
        stage('git repo & clean') {
            steps {
                bat "rmdir /s /q Harshitha_Jenkins_Maven || exit 0"
                bat "git clone https://github.com/Harshitha-Macha/Harshitha_Jenkins_Maven.git"
                bat "mvn clean -f Harshitha_Jenkins_Maven/pom.xml"
            }
        }
        stage('install') {
            steps {
                bat "mvn install -f Harshitha_Jenkins_Maven/pom.xml" 
            }
        }
        stage('test') {
            steps {
                bat "mvn test -f Harshitha_Jenkins_Maven/pom.xml"
            }
        }
        stage('package') {
            steps {
                bat "mvn package -f Harshitha_Jenkins_Maven/pom.xml"
            }
        }
    }
}


SCRIPTED PIPELINE:
node {
    stage('Checkout Source') {
        git url: 'https://github.com/savraam674/MavenJavaDemo.git', branch: 'master'
    }

    stage('Build') {
        echo "Running Maven Clean Install"
        bat "mvn clean install"
    }

    stage('Test') {
        echo "Running Maven Tests"
        bat "mvn test"
    }

    stage('Deploy') {
        echo "Deploy step (For Assignment Purpose Only)"
        echo "Deployment completed successfully!"
    }
}
