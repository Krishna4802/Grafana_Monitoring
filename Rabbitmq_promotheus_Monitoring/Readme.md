docker run -dit -p 9001:9001 -p 5432:5432 -p 15692:15692 -p 3000:3000 -p 9090:9090 -p 9854:9854 -p 9100:9100 --name rabbitmq ubuntu

apt update
apt install default-jre -y
apt-get install wget -y
apt install nano -y
apt install vim -y
apt install sudo -y
apt install rabbitmq-server -y


sudo apt update
sudo apt install -y gnupg2 curl software-properties-common
curl -fsSL https://packages.grafana.com/gpg.key|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/grafana.gpg
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
sudo apt update
sudo apt -y install grafana
sudo service grafana-server start


wget https://github.com/prometheus/prometheus/releases/download/v2.50.1/prometheus-2.50.1.linux-amd64.tar.gz
tar xvfz prometheus-2.50.1.linux-amd64.tar.gz


sudo nano /etc/rabbitmq/rabbitmq.config

[
    {rabbitmq_management, [
        {listener, [
            {port, 9001}
        ]}
    ]}
].


sudo rabbitmq-plugins enable rabbitmq_management
service rabbitmq-server start
sudo rabbitmqctl add_user admin admin
sudo rabbitmqctl set_user_tags admin administrator
sudo rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"


rabbitmq-plugins enable rabbitmq_prometheus


cd prometheus-2.50.1.linux-amd64
vi prometheus.yml

  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]

  - job_name: "rabbitmq"
    static_configs:
      - targets: ["localhost:15692"]
    
          
./prometheus


http://localhost:9090/targets -> Conformation
curl http://localhost:15692/metrics



Grafana dashboard id -> 10991


to return per-object (unaggregated) metrics 

    cat ./etc/rabbitmq/rabbitmq.conf
    prometheus.return_per_object_metrics = true
    management.listener.port = 9001



for verification : rabbitmqctl environment | grep prometheus


    output :  {prometheus,[]},
            {rabbitmq_prometheus,[{return_per_object_metrics,true}]},