node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      
      
      sh '''
         mvn clean package
      '''
   }
   
   stage('deploy') {
 
    echo "Azure Connection"
    	withCredentials([azureServicePrincipal('	ExcibitAzurePrincipalService')]) {
	    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
	    sh 'az account set -s $AZURE_SUBSCRIPTION_ID'
	    sh 'az resource list'
	} 
      sh '''      
        mvn azure-webapp:deploy 
      '''
   }
}
