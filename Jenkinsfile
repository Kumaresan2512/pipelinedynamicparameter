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
        // activeChoiceReactive(
        //     name: 'server',
        //     script: """
        //     def environment = input('Select the environment', choices: ['dev', 'uat', 'prod'])
        //     def servers = ['server1', 'server2', 'server3']
        //     if (environment == 'dev') {
        //         servers.remove('server3')
        //     }
        //     return servers
        //     """,
        //     description: 'Select the server to deploy to'
        // )
    }
    stages {
        stage('Select Options') {
            steps {
                script {
                    echo 'success'
                    // echo "lambda= $lambda"
                    // echo "ENV= $environment"
                    // if(lambda == "Catalog Selection")
                    // {     
                    //     awsLambdaConfig  = catalogselectionawsLambdaConfig
                    //     environmentOrder = catalogselectionenvironmentOrder                      
                    // }
                    // else 
                    // {
                    //     awsLambdaConfig  = technicalawsLambdaConfig
                    //     environmentOrder = technicalenvironmentOrder                      
                    // }

                    // println awsLambdaConfig
                    // println environmentOrder
                    // print params.environment
                    // print params.lambda
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
properties([
    parameters([
        [
            $class: 'ChoiceParameter',
            name: 'lambda',
            script: [
                $class: 'GroovyScript',
                script: [
                    script: '''return ['dcrdev', 'qa', 'dev', 'uat', 'stg', 'prod']'''
                ]
            ],
            choiceType: 'PT_SINGLE_SELECT',
            description: 'Select the base environment',
            randomName: 'choice-parameter-2'
        ],
        [
            $class: 'CascadeChoiceParameter',
            name: 'environment',
            description: 'Select the technical environment',
            script: [
                $class: 'GroovyScript',
                script: [
                    script: '''if (lambda == 'dcrdev') {return ['choice1-option1', 'choice1-option2', 'choice1-option3']} else if (lambda == 'qa') {return ['choice2-option1', 'choice2-option2']} else if (lambda == 'dev') {return ['choice3-option1', 'choice3-option2']} else if (lambda == 'uat') {return ['choice4-option1']} else if (lambda == 'stg') {return ['choice5-option1', 'choice5-option2']} else if (lambda == 'prod') {return ['choice6-option1']} else {return ['']}'''
                ]
            ],
            choiceType: 'PT_SINGLE_SELECT',
            referencedParameters: 'lambda',
            randomName: 'choice-parameter-1'
        ]        
    ])
])

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
