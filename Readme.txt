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
***Uncomment run_as_user parameter and set it as following.

run_as_user="nexus"

   15  vi /etc/systemd/system/nexus.service
Add the following contents to the unit file.

[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
User=nexus
Group=nexus
ExecStart=/app/nexus/bin/nexus start
ExecStop=/app/nexus/bin/nexus stop
User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target

   16  chkconfig nexus on
   17  systemctl start nexus
   18  systemctl restart nexus
   19  journalctl -xe
   20  SELinux is preventing /usr/lib/systemd/systemd from execute access on the file nexus.
   21  chcon -R -t bin_t /app/nexus/bin/nexus
   22  systemctl start nexus
   The above command will start the nexus service on port 8081. To access the nexus dashboard, visit http://:8081. 

   25  cat /app/sonatype-work/nexus3/admin.password


    5  
