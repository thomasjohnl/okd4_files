# Setup home lab

Create Bastion host
  Set IP address to .99.20
  Choose connect automatically in NIC settings
  sudo hostnamectl set-hostname bastion
  Add hostname.yourdomain hostname to /etc/hosts
  sudo dnf -y install bind bind-utils
  sudo dnf -y install epel-release
  sudo dnf -y update
  sudo dnf -y install git
  clone this repo
  edit the files as necessary for new hostname, domain name and ip addresses
  sudo cp named.conf /etc/named.conf
  sudo cp named.conf.local /etc/named/
  sudo mkdir /etc/named/zones
  sudo cp db* /etc/named/zones
  sudo systemctl enable named
  sudo systemctl start named
  sudo systemctl status named
  sudo firewall-cmd --permanent --add-port=53/udp
  sudo firewall-cmd --reload
  set dns server on NIC to 127.0.0.1
  sudo systemctl restart NetworkManager
  dig okd.local
  dig –x 192.168.1.210
  sudo dnf install haproxy -y
  sudo cp haproxy.cfg /etc/haproxy/haproxy.cfg
  sudo setsebool -P haproxy_connect_any 1
  sudo systemctl enable haproxy
  sudo systemctl start haproxy
  sudo systemctl status haproxy
  sudo firewall-cmd --permanent --add-port=6443/tcp
  sudo firewall-cmd --permanent --add-port=22623/tcp
  sudo firewall-cmd --permanent --add-service=http
  sudo firewall-cmd --permanent --add-service=https
  sudo firewall-cmd --reload
  sudo dnf install -y httpd
  sudo sed -i 's/Listen 80/Listen 8080/' /etc/httpd/conf/httpd.conf
  sudo setsebool -P httpd_read_user_content 1
  sudo systemctl enable httpd
  sudo systemctl start httpd
  sudo firewall-cmd --permanent --add-port=8080/tcp
  sudo firewall-cmd --reload
  curl localhost:8080
