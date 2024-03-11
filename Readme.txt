    # yum update
    2  yum install wget -y
    3  sudo yum install java-1.8.0-openjdk.x86_64 -y
    4  mkdir /app
    6  cd /app
    7  sudo wget -O nexus.tar.gz https://download.sonatype.com/nexus/3/latest-unix.tar.gz
    8  tar -xvf nexus.tar.gz
    9  mv nexus-3* nexus
   10  adduser nexus
   11  chown -R nexus:nexus /app/nexus
   12  chown -R nexus:nexus /app/sonatype-work
   13  vi  /app/nexus/bin/nexus.rc
   14  vi /app/nexus/bin/nexus.vmoptions
   15  vi /etc/systemd/system/nexus.service
   16  chkconfig nexus on
   17  systemctl start nexus
   18  systemctl restart nexus
   19  journalctl -xe
   20  SELinux is preventing /usr/lib/systemd/systemd from execute access on the file nexus.
   21  chcon -R -t bin_t /app/nexus/bin/nexus
   22  systemctl start nexus
   23  /app/sonatype-work/nexus3/admin.password
   24  /app/sonatype-work/nexus3/admin.password -f
   25  cat /app/sonatype-work/nexus3/admin.password


    5  
