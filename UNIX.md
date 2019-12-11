# Top ten commands

## simple command and processing text

        #!/bin/bash

        true=0
        false=1

        VERSION=7.3.7.0-8-9ad3650
        echo ${VERSION:0:3}                       # will print 7.3
        version=`echo ${VERSION} | cut -d- -f1`   # version will be 7.3.7.0
        buildNo=`echo ${VERSION} | cut -d- -f2`   # buildNo will be 8

        # procedure which push and pop the directory
        pushd ()
        {
            command pushd "$@" > /dev/null
        }

        popd ()
        {
            command popd "$@" > /dev/null
        }

        if [[ "x${VAR}" = "x" ]]; then
            echo -e "\nError. VAR is empty.\n\n"
            print_usage
            exit $false
        fi

        if [[ -f ${configfile} ]]; then
            . ${configfile}
        fi


## pipes

        mknod the_pipe p
        chmod 600 the_pipe
        nohup cat the_pipe | gzip > packed.gz &

        cat test_file.txt > the_pipe

        rm -f the_pipe

## trap

        TMPFILE=$(tempfile)
        trap 'echo "removing $TMPFILE"; rm -f $TMPFILE' INT TERM EXIT

## sh -e for clean code

        #!/bin/sh -e

        # If the command may fail and it is OK write it explicitily!
        false || true

        echo "false || true will not fail!"

        # false returns and error
        false

        echo "false will break the flow because of -e flag! When run without the flag it does not break!"

# Linux distro

        # Determine what distribution I have
        more /etc/issue

        # Install package using yum
        sudo yum install ${module}

        # Install package using apt-get
        sudo apt-get install ${module}

        # Download missing packages manually
        For Cent Os manually download from  http://mirror.centos.org/centos/6/os/x86_64/Packages/


# System and application monitoring

* http://newrelic.com/
* http://www.zabbix.com/
* http://www.cacti.net/
* http://www.nagios.org/

# Nice oneliners

|  How                          | What                                       |
|-------------------------------|--------------------------------------------|
|  netstat -tulpn               | Who is using my tcp/ip port                |
|  netstat -anobv               | Who is using my tcp/ip port on WINDOWS     |
|  ps -fu kazior                | Show me my processes (user is kazior)      |
|  ps -eo pid,lstart,cmd        | When my process started                    |


# xargs oneliners

    # IntelliJ Idea runs AppMainV2 application for normal run, and actual main for debug session
    jps -l | grep AppMainV2 | awk '{print $1}' | xargs -n1 jconsole
    jps -l | grep AppMainV2 | awk '{print $1}' | xargs -n1 jstack > j8


# binary compatibility verification

    # prepare verification hash
    find . -type f -print | sort | xargs md5sum > files-`date "+%Y-%m-%d_%H-%M-%S"`

# json in shell

    # thanks to http://stedolan.github.com/jq
    > cat file.json
    {
        "simple": {"property": "value 01"},
        "items": [{"name": "item 1"},
                  {"name": "item 2"},
                  {"name": "item 3"}]
    }

    > json .items[1].name  file.json
    "item 2"
    > json .simple.property  /home/dps/file.json
    "value 01"
    > json .simple.property  /home/dps/file.json |  tr -d '"'
    value 01

    # more complex

    CONFIG="$(cat file.json)"

    NUMBER_OF_ITEMS="$(echo $CONFIG | json '.items | length')"
    i=0
    while [ $i -lt $NUMBER_OF_ITEMS ]; do
        NAME="$(echo $CONFIG | json .items[$i].name | tr -d '"')"
        echo "Found: $NAME"
        i=$[$i+1]
    done



# Network connection diagnosis

    # ssl connection
    openssl s_client -connect 132.10.1.193:443

    # standard connection
    telnet 132.10.1.193 80

# links

* [Error codes]  http://zenit.senecac.on.ca/wiki/index.php/BASH_Exit_Status
* [BAsh hackers] http://wiki.bash-hackers.org/start

# putty tunnel from windows

    # through jump to dest host
    start C:\app\putty\putty.exe 10.131.2.12 -L 1521:10.131.2.12:1521 -l username -pw password

# JAVA_HOME on windows

    REM Will not work when path constains spaces (it is a just punishment for spaces)
    set JAVA_HOME=c:\app\java\jdk1.8.0_25\
    set PATH=%JAVA_HOME%\bin;%PATH%
    echo %PATH%
    java -version

# JAVA_HOME on linux

    JAVA_HOME=/opt/oracle-jdk-bin-1.8/
    PATH=$JAVA_HOME/bin:$PATH
    java -version

# delete all messages with mail

    # after https://stackoverflow.com/questions/7076186/how-do-i-purge-a-linux-mail-box-with-huge-number-of-emails
    mail -N
    d *
    quit

# jar listing

    jar tvf the.ear | grep junit  # search junit in the.ear

# other

## looping

    #!/bin/bash
    for i in {1..10}
    do
        echo $i
    done

## serving local files with oneliner using python http server

    # Python 2.x
    $ python -m SimpleHTTPServer 8000

    # Python 3.x
    $ python -m http.server 8000

## globstar instead of find

    find -type f -name "*.py" -exec wc -l {} \;
    shopt -s globstar
    wc -l **/*.py
