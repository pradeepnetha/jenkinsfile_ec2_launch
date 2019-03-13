pipeline {
    agent anychoice (choices: ['asg-new'] name: 'key_name')
        parameters {
        //string (description: 'enter ami_id', name: 'img_id')
        //string (description: 'enter Instance Type', name: 'instance_type')
        //string (description: 'enter subnet id', name: 'sub_id')
        //string (description: 'enter region name', name: 'region_name')
        //string (description: 'enter Security Group', name: 'sg_name')
        choice (choices: ['img_id'], description: 'choose key pair?', name: 'key_name')
        choice (choices: ['instance_type'], name: 'key_name')
        choice (choices: ['sub_id'], name: 'key_name')
        choice (choices: ['region_name'], name: 'key_name')
        choice (choices: ['sg_name'], name: 'key_name')    
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
           //sh '''
             //  chmod +x pradeepec2launch.sh
             ./pradeepec2launch.sh $img_id $instance_type $sub_id $region_name $sg_name $key_name
           //echo builded ${ InstanceId }
           //'''  
               
               
               // Show the select input modal
               //echo "${ ami_id }"
               //echo "${key_name}"
               
            }
//          withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-access', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
   // some block
               
               

        }         
           }
        }
}
