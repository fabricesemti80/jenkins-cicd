pipeline {
    agent any
    
    environment {
        ANSIBLE_IMAGE = 'alpine/ansible:latest'
    }
    
    stages {
        stage('Prepare Ansible Playbook') {
            steps {
                script {
                    // Create the Ansible playbook file and ensure it's readable
                    writeFile file: 'hello-world.yml', text: '''---
- hosts: localhost
  connection: local
  gather_facts: no
  tasks:
    - name: Print Hello World
      ansible.builtin.debug:
        msg: 'Hello World from Ansible in Docker!'

    - name: Create a simple output file
      ansible.builtin.copy:
        content: 'Ansible container is working!'
        dest: /apps/output.txt
'''
                    // Make sure the file exists and is readable
                    sh "ls -la hello-world.yml"
                }
            }
        }
        
        stage('Run Ansible and Verify Output') {
            steps {
                script {
                    // Pull the latest image
                    sh "docker pull ${ANSIBLE_IMAGE}"
                    
                    // Run the container with the playbook mounted
                    // Use absolute path to ensure the file is found
                    sh "docker run --rm -v \${PWD}:/apps ${ANSIBLE_IMAGE} ansible-playbook /apps/hello-world.yml"
                    
                    // The output file will be in the current directory
                    sh "cat output.txt || echo 'Output file not found'"
                }
            }
        }
    }
    
    post {
        always {
            echo 'Cleaning up...'
            sh 'rm -f hello-world.yml output.txt || true'
        }
        
        success {
            echo 'Ansible Docker pipeline completed successfully!'
        }
        
        failure {
            echo 'Pipeline failed. Check the logs for more information.'
        }
    }
}
