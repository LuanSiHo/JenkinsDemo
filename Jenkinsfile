pipeline {
    agent any

    environment {
    	ARCHIVED_PATH = "Archived"
    }

    stages {
    	stage("Initialization") {
    		echo "Initialization"
			sh "mkdir -p $WORKSPACE/$ARCHIVED_PAT"
    	}

    	stage("Code Cloning...") {
    		steps {
    			sh "rm -rf DSDVNCO"
    			script {
    				def branch = DSD_BRANCH.replaceAll('refs/heads/', '')
                    sh 'git clone https://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@https://github.com/LuanSiHo/DSD.git --branch '+ branch+''
    			}
    		}
    	}

    	stage("Clearing Cached files") {
    		steps {
    			    dir("${env.WORKSPACE}/DSDVNCO"){
                    sh 'rm -rf DSDVNCO.xcworkspace'
                    sh 'rm -f Podfile.lock'
                    sh 'rm -rf Pods'
                }
    		}
    	}
    }
}