pipeline {
    
    agent any

    
    stages {
        stage ('checkout') {
            steps {
                echo "This is checkout stage"
            }
        }
        stage ('build') {
            steps {
                echo "This is build stage"
            }
        }
        stage ('sonarscan') {
            steps {
                echo "This is sonarscan stage"
            }
        }               
        stage ('push') {
            steps {
                echo "This is push stage"
            }
        }
        stage ('deploy') {
            steps {
                echo "This is deploy stage"
            }
        }       
        stage('Build and Upload WAR') {
    steps {
        withCredentials([
            usernamePassword(
                credentialsId: 'jfrog-credentials',
                usernameVariable: 'JFROG_USER',
                passwordVariable: 'JFROG_TOKEN'
            )
        ]) {
            sh '''
                cat > settings.xml <<EOF
<settings>
    <servers>
        <server>
            <id>jfrog-releases</id>
            <username>${JFROG_USER}</username>
            <password>${JFROG_TOKEN}</password>
        </server>
    </servers>
</settings>
EOF

                mvn -B -s settings.xml clean deploy
                rm -f settings.xml
            '''
        }
    }
}
    }
}
