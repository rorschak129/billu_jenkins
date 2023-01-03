# Start by defining the pipeline using the `pipeline` directive.
pipeline {
    # Declare the environment variables used in this Jenkinsfile.
    environment {
        REGISTRY = 'docker.io'
        REPOSITORY = 'myrepo'
        IMAGE_NAME = 'myimage'
        TAG = 'latest'
    }
    # Declare the stages in the pipeline.
    stages {
        # The "Build" stage.
        stage('Build') {
            # Define the steps in this stage.
            steps {
                # Build the Docker image.
                sh '''
                    docker build -t $REGISTRY/$REPOSITORY/$IMAGE_NAME:$TAG .
                '''
            }
        }
        # The "Test" stage.
        stage('Test') {
            # Define the steps in this stage.
            steps {
                # Run the tests in the Docker image.
                sh '''
                    docker run -v $WORKSPACE:/app $REGISTRY/$REPOSITORY/$IMAGE_NAME:$TAG npm test
                '''
            }
        }
        # The "Publish" stage.
        stage('Publish') {
            # Define the steps in this stage.
            steps {
                # Push the Docker image to the registry.
                sh '''
                    docker push $REGISTRY/$REPOSITORY/$IMAGE_NAME:$TAG
                '''
            }
        }
        # The "Deploy" stage.
        stage('Deploy') {
            # Define the steps in this stage.
            steps {
                # Deploy the Docker image to the production environment.
                sh '''
                    docker run -d -p 80:80 $REGISTRY/$REPOSITORY/$IMAGE_NAME:$TAG
                '''
            }
        }
    }
}
