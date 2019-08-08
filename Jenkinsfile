pipeline {
    agent { label 'MASTER' }
        parameters {
            string(defaultValue: "inventory", description: 'Ansible Host file', name: 'INV_FILE')
            string(defaultValue: "GROUP_NAME", description: 'Ansible Host Group', name: 'INV_GRP')   
            
            string(defaultValue: "https://confluence.anthem.com/display/MST/Example", description: 'WSR URL', name: 'WSR_URL')                          
            string(defaultValue: 'YOUR_USER_ID', description: 'Artifictory User ID', name: 'MY_USERID')
            password(defaultValue: '', description: 'Artifactory Password', name: 'MY_PASSWORD')
    }
    stages {
        // stage('Cleanup Jenkins Job Workspace'){
        //     steps {
        //         step([$class: 'WsCleanup'])
        //     }
        // }       
        stage('Run Ansible Deploy operation'){        
            steps {            
            wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {
                    echo 'Validate Access'
                    ansiblePlaybook credentialsId: 'PASSKEY_TO_SERVER',
                    installation: 'ansible', 
                        inventory: '/Users/${MY_USERID}/${INV_FILE}',
                    limit: '${INV_GRP}',
                        playbook: '${WORKSPACE}/deploy_artifacts.yml',
                    colorized: true
                }
            }
        }
        stage('Demo Performance'){
            steps {
                echo 'Clap if you liked the demo!'
            }
        }

    }
}
