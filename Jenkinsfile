node {
  stage('Build Tasks') {
    openshift.withCluster() {
      openshift.withProject("na46-blue-green") {
        openshift.selector("bc", "green").startBuild("--wait=true")
      }
    }
  }
  stage('Tag Image') {
    openshift.withCluster() {
      openshift.withProject("na46-blue-green") {
        openshift.tag("blue", "green:${BUILD_NUMBER}")
      }
    }
  }
  stage('Deploy new image') {
    openshift.withCluster() {
      openshift.withProject("na46-blue-green") {
        openshift.selector("dc", "green").rollout().latest();
      }
    }
  }
}