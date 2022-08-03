pipeline{
 agent any
 stages{
   stage('checkout'){
    steps{
      checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'a8df228b-021f-4554-8c9c-18777bde22f7', url: 'git@github.com:bhavanaadmin/FoodAppCore.git']]])
    }
   }
   stage('Build'){
    steps{
     sh "pwd"
      dir('FoodAppCore/FoodApp') {
        sh "pwd"
    }
     sh "pwd"
     sh 'docker build -t gcr.io/gj-playground/food-app:yum .'
    }
   }
   stage('gcpcreds'){
    steps{
      withCredentials([file(credentialsId: 'a06a2af6-6e25-492d-a996-9b93891b6208', variable: 'GC_KEY')]) {
    sh("gcloud auth activate-service-account --key-file=${GC_KEY}")
    sh("gcloud auth configure-docker")
}
    }
   }
   stage('push'){
    steps{
     sh 'docker push gcr.io/gj-playground/food-app:yum'
    }
   }
 }
}
