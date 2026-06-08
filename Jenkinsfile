pipeline {
    agent any

    stages {

        stage("Clone") {
            steps {
                git url: "https://github.com/your-repo/sample-app.git", branch: "main"
            }
        }

        stage("Compile") {
            steps {
                echo "Compile ho gya"
                bat 'mvn compile'
            }
        }

        stage("Testing") {
            steps {
                echo "Testing ho gya"
                bat 'mvn test'
            }
        }

        stage("Package") {
            steps {
                echo "Packaging ho gya"
                bat 'mvn package'
            }
        }

        stage("Build") {
            steps {
                echo "Docker Build ho gya"
                bat 'docker build -t sample-app .'
            }
        }

        stage("Push") {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerHubCreds',
                        usernameVariable: 'dockerHubUser',
                        passwordVariable: 'dockerHubPass'
                    )
                ]) {
                    bat 'docker login -u %dockerHubUser% -p %dockerHubPass%'
                    bat 'docker tag sample-app %dockerHubUser%/sample-app:latest'
                    bat 'docker push %dockerHubUser%/sample-app:latest'
                }
            }
        }
    }
}