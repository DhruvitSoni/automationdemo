node()
    {
    stage('Cloning Git')
        {
            checkout scm
        }
        
    stage('Install dependencies') 
        {
            nodejs('nodejs') 
            {
                sh 'npm install'
                echo "Modules installed"
            }
        }
    stage('Build') 
    {
        nodejs('nodejs') 
        {
            sh 'npm run build'
            echo "Build completed"
        }   
    }
}

node('awsnode') 
{
    echo 'Unstash'
    unstash 'buildArtifacts'
    echo 'Artifacts copied'

    echo 'Copy'
    sh "yes | sudo cp -R bundle.tar.gz /var/www/html && cd /var/www/html && sudo tar -xvf bundle.tar.gz"
    echo 'Copy completed'
}
