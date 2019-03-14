pipeline {
    agent any
    environment {
        COMMITS_ON_MASTER = sh(script: 'var=$( cat instance1 )', returnStdout: true).trim()
    }
        parameters {
        //string (description: 'enter ami_id', name: 'img_id')
        //string (description: 'enter Instance Type', name: 'instance_type')
        //string (description: 'enter subnet id', name: 'sub_id')
        //string (description: 'enter region name', name: 'region_name')
        //string (description: 'enter Security Group', name: 'sg_name')
        choice (choices: ['ami-0b500ef59d8335eee'], description: 'choose key pair?', name: 'img_id')
        choice (choices: ['t2.micro'], name: 'instance_type')
        choice (choices: ['subnet-0e7e366cb34aca9b2'], name: 'sub_id')
        choice (choices: ['us-east-2'], name: 'region_name')
        choice (choices: ['sg-04a6d324940433647'], name: 'sg_name')    
        choice (choices: ['asg-new','CI_VPC', 'test1'], description: 'choose key pair?', name: 'key_name')
    }
    
    stages {
        
        stage ('build') {
           steps {
           withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', 
           accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
           credentialsId: 'aws key', 
           secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])  {    
           git url: 'https://github.com/pradeepnetha/ec2launch.git'
    
           sh '''
                chmod +x pradeepec2launch.sh
                ./pradeepec2launch.sh $img_id $instance_type $sub_id $region_name $sg_name $key_name
          '''
          sh 'aws ec2 describe-instances --filters "Name=tag:Name,Values=Web3" --region us-east-2 > instance'
               
          
          
          sh ' grep InstanceId instance > instance1 '
          sh([script: 'grep InstanceId instance > instance1'])
          sh([script: 'var=$( cat instance1 )'])
              
           //sh "echo $var"
               //echo "$var"
              /// sh 'echo $var'
         
              
              //echo "${InstanceId}"
            echo "There are ${env.COMMITS_ON_MASTER} commits on master"   
               
               // Show the select input modal
               //echo "${ ami_id }"
               //echo "${key_name}"
               
               slackSend message: 'build is success', tokenCredentialId: 'slack-jenkins'
            
            }
//          withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-access', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
   // some block
               
               

        }         
           }
       
        }
}
