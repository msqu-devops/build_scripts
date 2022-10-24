# Build Scripts > Gradle

## Gitlab Maven Repo

```gradle
// configure ids
buildscript {
    ext {
        gitlabCiApiUrl = System.getenv("CI_API_V4_URL") ?: "https://gitlab.com/api/v4"
        gitlabCiProjectId = System.getenv("CI_PROJECT_ID") ?: "TODO add project id for building outside CI here"
    }
}

// add script
apply from: 'https://raw.githubusercontent.com/dhswt/build-scripts/master/gradle/GitlabMavenRepo.gradle'

// configure a gitlab as a source
project {
    repositories {
        mavenCentral()
        mavenLocal()
        addGitlabGroupRepository(it, "<GROUP_NAME>", "<GROUP_ID>")
    }
}

// publish to gitlab
publishing {
    repositories {
        addGitlabPublishingRepository(it)
    }
    publications {
        maven(MavenPublication) {
            from components.java
        }
    }
}
```
