node {
  stage('Checkout') {
        checkout scm
  }

  stage('Build') {
        sh "./gradlew clean assemble test check jacocoTestReport"
  }

  stage('Report') {
        androidLint canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/lint-results.xml', unHealthy: '', unstableTotalAll: '0'
        step([$class: 'CheckStylePublisher', canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/reports/**/detekt.xml', unHealthy: '', unstableTotalAll: '0'])
        junit '**/test-results/normalDebug/junit-platform/*.xml'
        jacoco exclusionPattern: '**/R.class, **/R$*.class, **/*$ViewInjector*.*, **/BuildConfig.*, **/Manifest*.*, **/*Test*.*, android/**/*.*, androidx/**/*.*, **/*ViewModel_Factory.*, **/*_MembersInjector.class, **/Dagger*Component.class, **/Dagger*Component$**, **/Dagger*Component$Builder.class, **/*Module_*Factory.class, **/*Module.class, **/AndroidBuilder*.class', classPattern: '**/classes, **/tmp/kotlin-classes/normalDebug'
  }
}
