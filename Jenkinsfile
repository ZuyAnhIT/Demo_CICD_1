pipeline {
 agent any
 
 stages {
	stage('clone'){
		steps {
			echo 'Cloning source code'
			git branch:'main', url: 'https://github.com/ZuyAnhIT/Demo_CICD_1.git'
		}
	} // end clone

  } // end stages
}//end pipeline
