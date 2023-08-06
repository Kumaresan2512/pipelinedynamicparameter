pipeline {
    agent any

    stages {
        stage('Select Options') {
            steps {
                script {

                    echo "ENV= $environment"
                    echo "BRANCH= $git_branch"
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
