pipeline {
  agent any
  options {
    timeout(time: 30, unit: 'MINUTES')
  }
  stages {
    stage('Prepare') {
      steps {
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
      withCredentials([string(credentialsId: 'discord.webhook.channel', variable: 'WEBHOOK_CHANNEL')]) {
        withCredentials([string(credentialsId: 'discord.webhook.token', variable: 'WEBHOOK_TOKEN')]) {
          sh "curl -X POST --data '{ \"embeds\": [{\"title\": \"[DiscordIntegration][$BRANCH_NAME] Build $BUILD_DISPLAY_NAME : $currentBuild.currentResult\", \"type\": \"link\", \"url\": \"$BUILD_URL\", \"thumbnail\": { \"url\": \"https://build.chikachi.net/static/e0a4a1db/images/48x48/blue.png\" } }] }' -H \"Content-Type: application/json\"  https://discordapp.com/api/webhooks/$WEBHOOK_CHANNEL/$WEBHOOK_TOKEN"
        }
      }
    }
    unstable {
      withCredentials([string(credentialsId: 'discord.webhook.channel', variable: 'WEBHOOK_CHANNEL')]) {
        withCredentials([string(credentialsId: 'discord.webhook.token', variable: 'WEBHOOK_TOKEN')]) {
          sh "curl -X POST --data '{ \"embeds\": [{\"title\": \"[DiscordIntegration][$BRANCH_NAME] Build $BUILD_DISPLAY_NAME : $currentBuild.currentResult\", \"type\": \"link\", \"url\": \"$BUILD_URL\", \"thumbnail\": { \"url\": \"https://build.chikachi.net/static/e0a4a1db/images/48x48/yellow.png\" } }] }' -H \"Content-Type: application/json\"  https://discordapp.com/api/webhooks/$WEBHOOK_CHANNEL/$WEBHOOK_TOKEN"
        }
      }
    }
    failure {
      withCredentials([string(credentialsId: 'discord.webhook.channel', variable: 'WEBHOOK_CHANNEL')]) {
        withCredentials([string(credentialsId: 'discord.webhook.token', variable: 'WEBHOOK_TOKEN')]) {
          sh "curl -X POST --data '{ \"embeds\": [{\"title\": \"[DiscordIntegration][$BRANCH_NAME] Build $BUILD_DISPLAY_NAME : $currentBuild.currentResult\", \"type\": \"link\", \"url\": \"$BUILD_URL\", \"thumbnail\": { \"url\": \"https://build.chikachi.net/static/e0a4a1db/images/48x48/red.png\" } }] }' -H \"Content-Type: application/json\"  https://discordapp.com/api/webhooks/$WEBHOOK_CHANNEL/$WEBHOOK_TOKEN"
        }
      }
    }
  }
}
