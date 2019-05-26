node{
    @Library('library-pipeline')_
    def mvnHome
    currentBuild.result = "SUCCESS"
    try{
    stage('git_checkout'){
        git 'https://github.com/jprakash197/spring-boot-hello-world.git'
        sayHello 'Jyoti'
    }
    stage('sonar_code_quality_check'){
       // mvnHome=tool 'M3'
        //sonarCheck "$mvnHome",'jpsonar'
    }
    stage('maven_build'){
       // mavenBuild "$mvnHome"
    }
    stage('artifactory_upload'){
       // jfrogUpload 'jpart','*.jar','project_repo'
    }
    
    stage('docker_image_build'){
  //        dockerImageBuild 'jyoti_img'
    }
    
    stage('dockerhub_upload'){
   //       dockerUpload "$userNameDocker","$passwordDocker",'jyoti_img'
    }
    stage('image_run'){
        sh 'sudo docker rm -f jyoti_cntnr'
        sh 'sudo docker run -d -p 8086:8080 --n`ame jyoti_cntnr jyoti_img' 
    }
    }catch(caughtError){
            currentBuild.result = "FAILURE"
            mail (to: 'jyoti.behera@mindtree.com',
            subject: "Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) is failing",
            body: "Hi Jyoti, Please go to ${env.BUILD_URL}. This build is failing. Kindly fix");
    }
}
