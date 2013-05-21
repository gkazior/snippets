# maven

## How to skip the tests?

        # Use -DskipTests ex.
        mvn install -DskipTests

## How to build the project offline?

        # Use the -o option
        mvn -o install


## How to increase perm space?

        When you have "java.lang.OutOfMemoryError: PermGen space" error during the compilation

        # on Windows
        set MAVEN_OPTS=-Xmx2000m -XX:MaxPermSize=512m

        #On unix
        MAVEN_OPTS="-Xmx2000m -XX:MaxPermSize=512m"
