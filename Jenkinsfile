// properties([
//   parameters([
//     [
//       $class: 'ChoiceParameter',
//       choiceType: 'PT_SINGLE_SELECT',
//       name: 'Environment',
//       script: [
//         $class: 'ScriptlerScript',
//         scriptlerScriptId:'Environments.groovy'
//       ]
//     ],
//     [
//       $class: 'CascadeChoiceParameter',
//       choiceType: 'PT_SINGLE_SELECT',
//       name: 'Host',
//       referencedParameters: 'Environment',
//       script: [
//         $class: 'ScriptlerScript',
//         scriptlerScriptId:'HostsInEnv.groovy',
//         parameters: [
//           [name:'Environment', value: '$Environment']
//         ]
//       ]
//    ]
//  ])
// ])

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo "${params.Environment}"
        echo "${params.Host}"
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
                    classpath: [],
                    sandbox: true,
                    script: '''return ["Catalog Selection","Product Characteristics","Technical Documentation"]'''
                ],
                fallbackScript: [
                    classpath: [],
                    sandbox: true,
                    script: '''return['']'''
                ],
            ],
            choiceType: 'PT_SINGLE_SELECT',
            description: 'Choose the lambda',
            randomName: 'choice-lambda'
        ],
        [
            $class: 'CascadeChoiceParameter',
            name: 'environment',
            description: 'Choose the environment',
            script: [
                $class: 'GroovyScript',
                script: [
                    classpath: [],
                    sandbox: true,
                    script:
                            '''if (lambda.equals("Catalog Selection")) {
                               return ['dcrdev_test','dcrdev', 'qa', 'dev', 'uat', 'stg', 'prod']
                               }
                              else if (lambda.equals("Product Characteristics") || lambda.equals("Technical Documentation")) {
                              return ['dcrdev', 'qa', 'dev', 'uat', 'stg', 'prod']
                              }
                              else {
                              return [""]
                              }
                            '''
                ],
                fallbackScript: [
                    classpath: [],
                    sandbox: true,
                    script: '''return['']'''
                ],
            ],
            choiceType: 'PT_SINGLE_SELECT',
            referencedParameters: 'lambda',
            randomName: 'choice-environment'
        ],
        [
            $class: 'CascadeChoiceParameter',
            name: 'coverage',
            description: 'Choose the deployment coverage',
            script: [
                $class: 'GroovyScript',
                script: [
                    classpath: [],
                    sandbox: true,
                    script:
                            '''if (lambda.equals("Catalog Selection")) {
                                return ['all', 'image_uri', 'artifacts']
                                }
                                else if (lambda.equals("Product Characteristics") || lambda.equals("Technical Documentation")) {
                                return ['image_uri']
                                }
                                else {
                                return [""]
                                }
                            '''
                ],
                fallbackScript: [
                    classpath: [],
                    sandbox: true,
                    script: '''return['']'''
                ],
            ],
            choiceType: 'PT_SINGLE_SELECT',
            referencedParameters: 'lambda',
            randomName: 'choice-coverage'
        ],
        [
            $class: 'ChoiceParameter',
            name: 'mode',
            script: [
                $class: 'GroovyScript',
                script: [
                    classpath: [],
                    sandbox: true,
                    script: '''return ['compare', 'details', 'update']'''
                ],
                fallbackScript: [
                    classpath: [],
                    sandbox: true,
                    script: '''return['']'''
                ],
            ],
            choiceType: 'PT_SINGLE_SELECT',
            description: '''Mode to run.<br/>
                            'update' -> Update functions.<br/>
                            'compare' -> Compare function image and environment variables.<br/>
                            'details' -> View the function details<br/>''',
            randomName: 'choice-mode'
        ]
        // [$class: 'ChoiceParameter', 
        //     choiceType: 'PT_SINGLE_SELECT', 
        //     description: 'Select the Env Name from the Dropdown List', 
        //     filterLength: 1, 
        //     filterable: true, 
        //     name: 'Env', 
        //     randomName: 'choice-parameter-5631314439613978', 
        //     script: [
        //         $class: 'GroovyScript', 
        //         fallbackScript: [
        //             classpath: [], 
        //             sandbox: false, 
        //             script: 
        //                 'return[\'Could not get Env\']'
        //         ], 
        //         script: [
        //             classpath: [], 
        //             sandbox: false, 
        //             script: 
        //                 'return["Dev","QA","Stage","Prod"]'
        //         ]
        //     ]
        // ], 
        // [$class: 'CascadeChoiceParameter', 
        //     choiceType: 'PT_SINGLE_SELECT', 
        //     description: 'Select the Server from the Dropdown List', 
        //     filterLength: 1, 
        //     filterable: true, 
        //     name: 'Server', 
        //     randomName: 'choice-parameter-5631314456178619', 
        //     referencedParameters: 'Env', 
        //     script: [
        //         $class: 'GroovyScript', 
        //         fallbackScript: [
        //             classpath: [], 
        //             sandbox: false, 
        //             script: 
        //                 '''return[\'Could not get Environment from Env Param\']'''
        //         ], 
        //         script: [
        //             classpath: [], 
        //             sandbox: false, 
        //             script: 
        //                 ''' if (Env.equals("Dev")){
        //                         return["devaaa001","devaaa002","devbbb001","devbbb002","devccc001","devccc002"]
        //                     }
        //                     else if(Env.equals("QA")){
        //                         return["qaaaa001","qabbb002","qaccc003"]
        //                     }
        //                     else if(Env.equals("Stage")){
        //                         return["staaa001","stbbb002","stccc003"]
        //                     }
        //                     else if(Env.equals("Prod")){
        //                         return["praaa001","prbbb002","prccc003"]
        //                     }
        //                 '''
        //         ]
        //     ]
        // ]
    ])
])