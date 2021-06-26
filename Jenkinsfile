pipeline {
    agent any

    environment {
    	ARCHIVED_PATH = "Archived"
    	PROJECT_NAME = "DSDVNCO"
    	LANG = "en_US.UTF-8"
    	PATH = "/Library/Frameworks/Python.framework/Versions/3.9/bin:/Library/Frameworks/Python.framework/Versions/3.7/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin:/Users/hosiluan/iOS/flutter/bin"
    }

    stages {
    	stage("Initialization") {
    		steps {
    			echo "Initialization"
				sh "mkdir -p $WORKSPACE/$ARCHIVED_PATH"
				sh "mkdir -p $WORKSPACE/$PROJECT_NAME"
    		}
    	}

    	stage("Code Cloning...") {
    		steps {
    			sh "rm -rf $PROJECT_NAME"
    			script {
    				def branch = DSD_BRANCH.replaceAll('refs/heads/', '')
                    sh 'git clone https://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:x-oauth-basic@github.com/LuanSiHo/DSD.git --branch '+ branch +' $PROJECT_NAME'
    			}
    		}
    	}

    	stage("Clearing Cached files") {
    		steps {
    			    dir("${env.WORKSPACE}/$PROJECT_NAME"){
                    sh 'rm -rf $PROJECT_NAME.xcworkspace'
                    sh 'rm -f Podfile.lock'
                    sh 'rm -rf Pods'
                }
    		}
    	}

    	stage("Installing pod") {
    		steps {
    			    dir("${env.WORKSPACE}/$PROJECT_NAME"){
					sh '''
                    security unlock-keychain -p 123456
                    pod install
                    '''
    			}
    		}
    	}

    	stage("Archiving") {
    		steps {
	    		dir("$env.WORKSPACE/$PROJECT_NAME") {
	    			sh '''
	    				security unlock-keychain -p 123456
	    				xcodebuild 
							-workspace ${env.WORKSPACE}/$PROJECT_NAME/$PROJECT_NAME.xcworkspace
	    					-scheme $PROJECT_NAME clean archive
	    					-configuration release
	    					-sdk iphoneos
	    					-archivePath ${env.WORKSPACE}/$ARCHIVED_PATH/$PROJECT_NAME.xcarchive
	    			'''
	    		}
    		}
    	}
    }
}