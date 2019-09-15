node{
   
   stage("App Build started"){
      echo 'App build started..'
      git credentialsId: 'Github-ID', url: 'https://github.com/itrain1/python-docker-app-openshift.git'
      }
   
   stage('Docker Build') {
     def app = docker.build "anandbk1/python-newrelic"
    }
   
   stage("Tag & Push image"){
      withDockerRegistry([credentialsId: 'dockerID',url: ""]) {
          sh 'docker tag manee2k6/py-spartans anandbk1/python-newrelic:dev'
          sh 'docker push anandbk1/python-newrelic:dev'
          sh 'docker push anandbk1/python-newrelic:latest'
      }
    }
   
   stage("App deployment started"){
     sh 'oc login --token=AUeAqkp8CQOqlTgbqbSv_PlvL_TxuDGQbtqDVtRQRvE --server=https://api.us-west-1.starter.openshift-online.com:6443'
     sh 'oc project jenkin-openshift'
     sh 'oc new-app --name py-anand anandbk1/python-newrelic'
      sh 'oc rollout latest dc/py-anand -o json' 
      sh 'oc rollout latest anandbk1/python-newrelic --name python \
          --env NEWRELIC_LICENSE=f8e0ea62a1e411cdcc3f60f93324a7c497f84a27 \
                NEWRELIC_APPNAME=pyapp2'
     //sh 'oc expose svc py-mani' 
    }
   
    stage('App deployed to Openshift environment') {
     echo 'App deployed to Openshift environment..'
    }

  }
