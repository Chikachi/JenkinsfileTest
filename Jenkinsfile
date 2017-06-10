pipeline {
  agent any
  options {
    timeout(time: 30, unit: 'MINUTES')
  }
  stages {
    stage('Prepare') {
      steps {
        checkout scm
        echo "Prepare"
      }
    }
    stage('Build') {
      steps {
        echo "Build"
      }
    }
    stage('Archive') {
      steps {
        echo "Archive"
      }
    }
  }
  post {
    success {
      sh "curl -X POST --data '{ \"embeds\": [{\"title\": \"Topic Title\", \"url\": \"https://example.com\", \"description\": \"This is a test for webhooks\", \"type\": \"link\", \"thumbnail\": {\"url\": \"https://camo.githubusercontent.com/9a1fd49e0c838517e1f6b476bf3514939383f7f3/687474703a2f2f6d656469612d656c657269756d2e637572736563646e2e636f6d2f617661746172732f34362f3335372f3633363035333537383336353435383238362e706e67\"}}] }' -H \"Content-Type: application/json\"  https://discordapp.com/api/webhooks/${credentials('discord.webhook.channel')}/${credentials('discord.webhook.token')}"
    }
  }
}
