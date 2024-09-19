## Airflow-Installation

    apt-get update
    apt-get install software-properties-common -y
    apt-add-repository universe 
    apt-get update
    apt install python3-pip
    apt-get install python-setuptools
    apt install python3-pip -y
    pip3 install apache-airflow
  
### modify the sollwing in airflow.cfg file
      postgresql://grafana:garfana@localhost:54332/airflow
***        
    airflow db init
    airflow users create --username admin --firstname admin --lastname testing --role Admin --email admin@domain.com
    airflow webserver -p 9000


## Monitoring Airflow with grafana

### configuration modification

**file location :** vi ~/airflow/airflow.cfg

      statsd_on = True
      statsd_host = localhost
      statsd_port = 8125
      statsd_prefix = airflow


## statsd enabling
    git clone https://github.com/prometheus/statsd_exporter.git
    cd /statsd_exporter
    make
    ./statsd_exporter --statsd.listen-udp=:9125 --web.listen-address=:9102

## Grafana DashBoard links
   https://github.com/databand-ai/airflow-dashboards/tree/main/grafana
