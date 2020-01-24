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

