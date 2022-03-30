node {
    checkout scm

    // deploy env dev
    docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
        sshagent (credentials: ['ssh-dev']) {
            sh 'mkdir -p ~/.ssh'
            sh 'ssh-keyscan -H "44.202.114.4" > ~/.ssh/known_hosts'
            sh "rsync -rav --delete ./ ubuntu@44.202.114.4:/home/ubuntu/dev.kelasdevops.xyz/ --exclude=.env --exclude=storage --exclude=.git"
            sh "ssh ubuntu@44.202.114.4 'cd ~/dev.kelasdevops.xyz/ && rm composer.lock && composer install'"
        }
    }

    // Testing
    docker.image('ubuntu').inside('-u root') {
       sh 'echo "Ini adalah test"'
    }

    // deploy env prod
    docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
        sshagent (credentials: ['ssh-prod']) {
            sh 'mkdir -p ~/.ssh'
            sh 'ssh-keyscan -H "44.202.114.4" > ~/.ssh/known_hosts'
            sh "rsync -rav --delete ./ ubuntu@44.202.114.4:/home/ubuntu/prod.kelasdevops.xyz/ --exclude=.env --exclude=storage --exclude=.git"
            sh "ssh ubuntu@44.202.114.4 'cd ~/prod.kelasdevops.xyz/ && rm composer.lock && composer install'"
        }
    }
}
