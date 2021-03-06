# maven

## How to skip the tests?

        # Use -DskipTests ex.
        mvn clean install -DskipTests
        
## How to disable colors for specs2

        mvn clean install -Dspecs2.commandline=nocolor

## How to download sources when project is generated?

        mvn idea:idea       -DdownloadSources=true -DdownloadJavadocs=true
        mvn eclipse:eclipse -DdownloadSources=true -DdownloadJavadocs=true

## How to build the project offline?

        # Use the -o option
        mvn -o install


## How to increase perm space?

        When you have "java.lang.OutOfMemoryError: PermGen space" error during the compilation

        # on Windows
        set MAVEN_OPTS=-Xmx2000m -XX:MaxPermSize=512m

        #On unix
        MAVEN_OPTS="-Xmx2000m -XX:MaxPermSize=512m"


## Working with shapshots?

        Try -U flag which updates shanpshots you have in your local repo.

        mvn -U install
        mvn -U clean install -DskipTests

## Analyze dependencies for a given library

        ## --batch-mode for no colors which are hard to read because of control characters 
        ## --includes since we want only one dependency
        mvn --batch-mode dependency:tree -Dverbose -Dincludes="com.ning:async-http-client" > output.tree.txt

## Continue compilation from the failed module 
        
        mvn clean install -Dtests.skip=true -rf :failedProject

## Speed up compilation with zinc

        zinc -J-Xmx4g -nailed -start

## Why not to read the command line help?

        usage: mvn [options] [<goal(s)>] [<phase(s)>]

        Options:
         -am,--also-make                        If project list is specified, also
                                                build projects required by the
                                                list
         -amd,--also-make-dependents            If project list is specified, also
                                                build projects that depend on
                                                projects on the list
         -B,--batch-mode                        Run in non-interactive (batch)
                                                mode
         -C,--strict-checksums                  Fail the build if checksums don't
                                                match
         -c,--lax-checksums                     Warn if checksums don't match
         -cpu,--check-plugin-updates            Ineffective, only kept for
                                                backward compatibility
         -D,--define <arg>                      Define a system property
         -e,--errors                            Produce execution error messages
         -emp,--encrypt-master-password <arg>   Encrypt master security password
         -ep,--encrypt-password <arg>           Encrypt server password
         -f,--file <arg>                        Force the use of an alternate POM
                                                file.
         -fae,--fail-at-end                     Only fail the build afterwards;
                                                allow all non-impacted builds to
                                                continue
         -ff,--fail-fast                        Stop at first failure in
                                                reactorized builds
         -fn,--fail-never                       NEVER fail the build, regardless
                                                of project result
         -gs,--global-settings <arg>            Alternate path for the global
                                                settings file
         -h,--help                              Display help information
         -l,--log-file <arg>                    Log file to where all build output
                                                will go.
         -N,--non-recursive                     Do not recurse into sub-projects
         -npr,--no-plugin-registry              Ineffective, only kept for
                                                backward compatibility
         -npu,--no-plugin-updates               Ineffective, only kept for
                                                backward compatibility
         -nsu,--no-snapshot-updates             Suppress SNAPSHOT updates
         -o,--offline                           Work offline
         -P,--activate-profiles <arg>           Comma-delimited list of profiles
                                                to activate
         -pl,--projects <arg>                   Comma-delimited list of specified
                                                reactor projects to build instead
                                                of all projects. A project can be
                                                specified by [groupId]:artifactId
                                                or by its relative path.
         -q,--quiet                             Quiet output - only show errors
         -rf,--resume-from <arg>                Resume reactor from specified
                                                project
         -s,--settings <arg>                    Alternate path for the user
                                                settings file
         -T,--threads <arg>                     Thread count, for instance 2.0C
                                                where C is core multiplied
         -t,--toolchains <arg>                  Alternate path for the user
                                                toolchains file
         -U,--update-snapshots                  Forces a check for updated
                                                releases and snapshots on remote
                                                repositories
         -up,--update-plugins                   Ineffective, only kept for
                                                backward compatibility
         -V,--show-version                      Display version information
                                                WITHOUT stopping build
         -v,--version                           Display version information
         -X,--debug                             Produce execution debug output
