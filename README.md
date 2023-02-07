# monitoring-promethues-grafana
Setting up Prometheus and Grafana in AWS 

Here is a step-by-step guide to install and configure Prometheus on an AWS EC2 instance:

Launch an EC2 instance: Choose a Linux-based AMI and make sure it has sufficient resources (such as CPU, memory, and storage) to run Prometheus.

Connect to the EC2 instance: You can use an ssh client like PuTTY to connect to the instance.

Install Prometheus: The simplest way to install Prometheus is to use the official Prometheus repository. You can add the repository to the instance by running the following commands:

#################################
sudo useradd --no-create-home --shell /bin/false prometheus
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
sudo chown prometheus:prometheus /etc/prometheus
sudo chown prometheus:prometheus /var/lib/prometheus
############################################



cd /tmp
curl -LO https://github.com/prometheus/prometheus/releases/download/v2.23.0/prometheus-2.23.0.linux-amd64.tar.gz
tar xvf prometheus-2.23.0.linux-amd64.tar.gz
sudo cp prometheus-2.23.0.linux-amd64/prometheus /usr/local/bin/
sudo cp prometheus-2.23.0.linux-amd64/promtool /usr/local/bin/
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool


Configure Prometheus: Create a configuration file for Prometheus in /etc/prometheus/prometheus.yml. The file should specify the targets you want to monitor and any additional configuration options you need. For example:

global:
  scrape_interval:     15s 
  evaluation_interval: 15s 

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
      
      
Start Prometheus: Start the Prometheus service by running the following command:

sudo service prometheus start 

Check Prometheus: You can check if Prometheus is running by accessing the Prometheus web UI at http://<EC2-instance-public-DNS>:9090.

(Optional) Secure Prometheus: You can secure Prometheus by using SSL/TLS encryption and authentication. This can be done by configuring reverse proxy software such as Nginx or Apache to act as a frontend for Prometheus.

  
  for prometheus node setup and Grafana setup
  
  https://devops4solutions.com/monitoring-using-prometheus-and-grafana-on-aws-ec2/
  
