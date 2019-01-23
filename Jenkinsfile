agent {
  node('master') {
    properties([
      [$class: 'BuildBlockerProperty',
       blockLevel: 'GLOBAL',
       blockingJobs: '*',
       scanQueueFor: 'ALL',
       useBuildBlocker: true],
     disableConcurrentBuilds(),
     [$class: 'BuildDiscarderProperty', 
        strategy: [
          $class: 'LogRotator', 
          daysToKeepStr: '10'
        ]
      ]
    ])

    stage('Checkout') {
      checkout scm
    }

    stage('Build') {
      sh 'pwd > workspace.txt'
      jobDsl targets: ['jobdsl/**/*.groovy'].join('\n'),
        removedJobAction: 'DELETE',
        removedViewAction: 'DELETE',
        ignoreExisting: false,
        sandbox: false
    }
  }
}