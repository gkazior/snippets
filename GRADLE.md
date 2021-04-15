# Gradle nice snippets 

## addinig test sources from non-standard directory - manualTest 

    sourceSets  {
        test {
            scala {
                srcDirs 'src/test/scala'
                srcDirs 'src/manualTest/scala'
            }
        }
    }
 
## running only one task from one submodule

    # where pim-tum-itests is a module
    # and the last part of a snake is a task to execute (test)
    ./gradlew :core:bss-backend:integrations:pim-tum:pim-tum-itests:test --no-build-cache


## nice plugins

    plugins {
      id 'nu.studer.credentials' version '1.0.7'
      id 'idea'
      id 'org.owasp.dependencycheck' version '5.3.2.1'
      id "org.jetbrains.gradle.plugin.idea-ext" version "0.7"
      id 'com.savvasdalkitsis.module-dependency-graph' version '0.9'
      id 'com.bmuschko.docker-remote-api'
    } 
