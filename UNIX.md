# Top ten commands

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

|  How                | What |
|---------------------|---------------------|
|  netstat -tulpn     | Who is using my tcp/ip port                |
|  netstat -anobv     |  Who is using my tcp/ip port on WINDOWS    |
|  ps -fu kazior      | Show me my processes (user is kazior)      |

# Network connection diagnosis

    # ssl connection
    openssl s_client -connect 132.10.1.193:443

    # standard connection
    telnet 132.10.1.193 80

# links

* [Error codes]  http://zenit.senecac.on.ca/wiki/index.php/BASH_Exit_Status
* [BAsh hackers] http://wiki.bash-hackers.org/start
