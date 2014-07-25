# Top ten commands

## pipes

        mknod the_pipe p
        chmod 600 the_pipe
        nohup cat the_pipe | gzip > packed.gz &

        cat test_file.txt > the_pipe

        rm -f the_pipe

# Linux distro

  Determine what distribution I have:
  more /etc/issue

  Install using yum
  sudo yum install ${module}

  Install using apt-get
  sudo apt-get install ${module}

  Download missing packages manually
  For Cent Os manually download from  http://mirror.centos.org/centos/6/os/x86_64/Packages/

# links

* [Error codes] http://zenit.senecac.on.ca/wiki/index.php/BASH_Exit_Status
