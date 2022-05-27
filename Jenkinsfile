pipeline{
  agent any

  stages{
          
    stage('Check spelling') {
      agent {
        dockerfile {
        filename 'Dockerfile.mdspell'
        args '-u="root" -v $WORKSPACE:/srv/jekyll -w /srv/jekyll --entrypoint=""'
        }
      }
      steps {
        echo "Check spelling"
        sh '''
          mdspell -V
          find . -name "*.md" | xargs mdspell -n -a -r --en-us --dictionary dicts/en_US-large
        '''
      }
    }
          
    stage('Node Linting') {
      agent {
        dockerfile {
        filename 'Dockerfile.linting'
        } 
      } 
      steps {
        sh '''
          eslint *.js
          node index.js
        '''
	    }
    }

    stage('Unit Testing') {
		  agent {
        dockerfile {
          filename  'Dockerfile.testing'
        }
      }   
      steps {
        echo 'This is Unit Testing...' 
			  sh '''
		      npm install jest
	        npm run test
	      '''
        }
	    }        
  }
} 
