catalogselectionawsLambdaConfig = [
    'dcrdev_test': ['accountID':'12345678', 'functionName': 'cs-documentation-ai-dev'],
    'dcrdev': ['accountID':'12345678', 'functionName': 'cs-documentation-ai-devcd'],
    'qa': ['accountID':'23456789', 'functionName': 'cs-documentation-devcd'],
    'dev': ['accountID':'2345678911', 'functionName': 'cs-documentation-dev'],
    'uat': ['accountID':'23456789111', 'functionName': 'cs-documentation-uat'],
    'stg': ['accountID':'234567891111', 'functionName': 'cs-documentation-stg'],
    'prod': ['accountID':'234567891111', 'functionName': 'cs-documentation-prod'],
]

technicalawsLambdaConfig = [
    'dcrdev': ['accountID':'12345678', 'functionName': 'technical-documentation-dev'],
    'qa': ['accountID':'23456789', 'functionName': 'technical-documentation-devcd'],
    'dev': ['accountID':'2345678911', 'functionName': 'technical-documentation-dev'],
    'uat': ['accountID':'23456789111', 'functionName': 'technical-documentation-uat'],
    'stg': ['accountID':'234567891111', 'functionName': 'technical-documentation-stg'],
    'prod': ['accountID':'234567891111', 'functionName': 'technical-documentation-prod'],
]
catalogselectionenvironmentOrder = ['dcrdev_test','dcrdev', 'qa', 'dev', 'uat', 'stg', 'prod']
technicalenvironmentOrder = ['dcrdev', 'qa', 'dev', 'uat', 'stg', 'prod']
awsLambdaConfig = []
environmentOrder = []
pipeline {
    agent any
        parameters {
        choice(
            name: 'coverage',
            choices: ['all', 'image_uri', 'artifacts'],
            description: 'Choose the deployment coverage'
        )
        choice(
            name: 'mode',
            choices: ['compare', 'details', 'update'],
            description: """
            Mode to run.<br>
            'update'  -> Update functions.<br>
            'compare' -> Compare function image and environment variables.<br>
            'details' -> View the function details
            """
        )
    }
    stages {
        stage('Select Options') {
            steps {
                script {
                    echo "lambda= $lambda"
                    echo "ENV= $environment"
                    if(lambda == "Catalog Selection")
                    {     
                        awsLambdaConfig  = catalogselectionawsLambdaConfig
                        environmentOrder = catalogselectionenvironmentOrder                      
                    }
                    else 
                    {
                        awsLambdaConfig  = technicalawsLambdaConfig
                        environmentOrder = technicalenvironmentOrder                      
                    }

                    println awsLambdaConfig
                    println environmentOrder
                    print params.environment
                    print params.lambda
					//echo params.environment
                    // Define the first choice parameter
                    // def firstChoice = input(
                    //     id: 'firstChoice',
                    //     message: 'Select the first option:',
                    //     parameters: [
                    //         choice(name: 'FirstOption', choices: ['OptionA', 'OptionB', 'OptionC'], description: 'Select an option')
                    //     ]
                    // )

                    // Define the second choice parameter based on the first choice
                    // def secondChoices = getSecondChoices(firstChoice)

                    // def secondChoice = input(
                    //     id: 'secondChoice',
                    //     message: 'Select the second option:',
                    //     parameters: [
                    //         choice(name: 'SecondOption', choices: secondChoices, description: 'Select an option')
                    //     ]
                    // )

                    // Continue with your pipeline using the selected options
                    //echo "First Option: ${firstChoice}"
                    //echo "Second Option: ${secondChoice}"
                }
            }
        }
    }
}

// Function to generate second choices based on the first choice
def getSecondChoices(firstChoice) {
    switch (firstChoice) {
        case 'OptionA':
            return ['OptionA1', 'OptionA2', 'OptionA3']
        case 'OptionB':
            return ['OptionB1', 'OptionB2']
        case 'OptionC':
            return ['OptionC1', 'OptionC2', 'OptionC3', 'OptionC4']
        default:
            return []
    }
}

def setEnvironment()
{	if(lambda == "Product Characteristics")
		return technicalawsLambdaConfig
}
