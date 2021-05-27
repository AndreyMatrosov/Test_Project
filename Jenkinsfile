node ('master') {
    stage('Checkout') {
           cleanWs()
           checkout([$class: 'GitSCM',
                   branches: [[name: '*/master']],
                   extensions: [],
                   userRemoteConfigs: [[credentialsId: 'jenkins_ssh',
                   url: 'https://github.com/AndreyMatrosov/curl']]])
    }
    withEnv(['CC=/usr/bin/make']) {
        stage('Build') {
            cmakeBuild(buildDir: 'build',
                   generator: 'Unix Makefiles',
                   buildType: 'Release',
                   installation: 'InSearchPath',
                   sourceDir: 'CMakeLists.txt')
        }
    }
    stage('Test') {
        ctest installation: 'CMake', workingDir: 'tests/unit'
    }
}
