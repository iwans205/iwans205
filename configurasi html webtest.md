pipeline {
   agent {label 'webtest-10.10.19.239'}

   environment { 
        BRANCH_NAME_BUILD = 'master'
        BRANCH_NAME_LOG = '/home/iwan/nodejs-log/jenkins-master.log'
    }
     
   stages {
      stage('building') {
         //when { 
         //    changeRequest authorEmail: "kristiono.setyadi@mncgroup.com"
        // }
         steps {
            git branch: 'master' , changelog: false, credentialsId: 'testing_jenkins', poll: false, url: 'ssh://git@allyoucaneat.visionplus.id:45817/website/html5.git'
            script {
            sh("git pull origin $BRANCH_NAME_BUILD")
            }
         }
      }
    stage('building-quasar+npm') {
          steps {
              script{
                try{
                    sh("npm install")
                    sh("quasar build -m ssr")
          }
                catch (err) {
                    sh("npm install '@babel/compat-data' ")
                    sh("quasar build -m ssr")
              }
         }
          }
          
      }
      stage('pm2 start / restart'){
   
          steps {
              script {
                  try {
                        sh("pm2 restart jenkins-$BRANCH_NAME_BUILD")
                     }
                  catch(err){
                        sh("pm2 start dist/ssr/index.js --name jenkins-$BRANCH_NAME_BUILD  --log $BRANCH_NAME_LOG" )
 
                     }
                }

          }
      }
      stage('git log '){
          steps{
              sh("git log -10")
          }
      }
    }

    post { 
        unsuccessful { 
            echo 'this code // still in progress'
        }
        
                                success { 
                            script{
                                    sh ( "git log -6 > /home/iwan/gitlog-webtest-html5.txt" )
                                    sh """
                                    curl -F document=@"/home/iwan/gitlog-webtest-html5.txt" https://api.telegram.org/bot1845698869:AAFHv9R1MH-119CjEv8mLAM3x_GPXDFDEGY/sendDocument?chat_id=-519351672
                                    """
                            }
                }

    }
}
