# front-end
#!/bin/bash
sudo yum -y install httpd
cd /var/www/html
echo "healthy" | sudo tee /var/www/html/healthy.html
sudo yum -y install git
cd /home/ec2-user
git clone https://github.com/sshariqrizvi15/front-end.git
sudo cp /home/ec2-user/front-end/vww/index.html /var/www/html/index.html
echo 'ProxyPreserveHost On' | sudo tee -a /etc/httpd/conf/httpd.conf
echo 'ProxyPass /app/checkRequest http://10.0.2.246:5000/app/checkRequest' | sudo tee -a /etc/httpd/conf/httpd.conf
echo 'ProxyPassReverse /app/checkRequest http://10.0.2.246:5000/app/checkRequest' | sudo tee -a /etc/httpd/conf/httpd.conf
sudo service httpd start
