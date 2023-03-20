
// it is a comment
pipeline{
 tools{
        // mymaven is coming from global tool configuration
        maven 'mymaven'
    }
 // ** which server/agent should this pipeline tasks be executed **
 agent any
 
 parameters {
 string(name: 'gitrepo', defaultValue: 'https://github.com/Sonal0409/DevOpsCodeDemo.git', description: 'enter the giturl')
 }
 
 stages {
     
     // stage is nothing but a job/task
     
     stage('1.CloneRepo')
     {
         steps{
           
           git "${params.gitrepo}"
         }
     }
     
     stage('2.CompileCode')
     {
         steps{
             // give the maven GOAL to compile: mvn compile
             
             sh 'mvn compile'
         }
     }
     
     stage('3.Codereview')
     {
         steps{
             
             catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                 
             sh 'mvn pmd:pmd'
             
             }
            
         }
     }
     
     stage('4.UnitTest')
     {
         steps{
             sh 'mvn test'
         }
        post{
            success{
               junit 'target/surefire-reports/*.xml' 
            }
        }
     }
     
     stage('5.Package')
     {
         steps{
             sh 'mvn package'
         }
     }
 }
    
}




    
