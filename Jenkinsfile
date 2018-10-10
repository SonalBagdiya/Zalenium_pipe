pipeline {
    agent any 
    stages {
        stage('Kubernetes cluster creation') {
            steps {
		    dir ('cookbooks'){
			    git 'https://github.com/kishan0001/chef_cookbooks.git'
			    sh 'sudo chef-client --local-mode --runlist "recipe[to_create_kubernetes_cluster_pipe]"'
		}      
            }
        }
    	stage('Zalenium hub deployment') {
            steps {
		    dir ('cookbooks'){
			    git 'https://github.com/kishan0001/chef_cookbooks.git'
			    sh 'sudo chef-client --local-mode --runlist "recipe[zalenium_deployment_pipe]"'
		}      
            }
        }
	 stage('Selenium grid script execution') {
            parallel {
                stage('Parallel Test-1') {
                    steps {
                        dir ('cookbooks'){
			    	git 'https://github.com/kishan0001/chef_cookbooks.git'
			    	sh 'sudo chef-client --local-mode --runlist "recipe[execute_selenium_script_1_pipe]"'
		        }      
                    }
                }
                stage('Parallel Test-2') {
                    steps {
                        dir ('cookbooks'){
			     	git 'https://github.com/kishan0001/chef_cookbooks.git'
			     	sh 'sudo chef-client --local-mode --runlist "recipe[execute_selenium_script_2_pipe]"'
			}
                    }
                }
            }
        }
	    stage('Kubernetes cluster destroy') {
            steps {
		    dir ('cookbooks'){
			    git 'https://github.com/kishan0001/chef_cookbooks.git'
			    sh 'sudo chef-client --local-mode --runlist "recipe[kubernetes_cluster_destroy_pipe]"'
		}      
            }
        }
	    stage('Delete created shell scripts') {
            steps {
		    dir ('cookbooks'){
			    git 'https://github.com/kishan0001/chef_cookbooks.git'
			    sh 'sudo chef-client --local-mode --runlist "recipe[to_delete_files_pipe]"'
		}      
            }
        }
	    stage('Clear docker images and containers') {
            steps {
		    dir ('cookbooks'){
			    git 'https://github.com/kishan0001/chef_cookbooks.git'
			    sh 'sudo chef-client --local-mode --runlist "recipe[to_clear_docker_images_container_pipe]"'
		}      
            }
        }
    }
}
