# Rabbitmq-installation-and-monitoring

## Airflow rabbit-mq installation

    apt install rabbitmq-server -y
 ***   
    sudo nano /etc/rabbitmq/rabbitmq.config

          [
              {rabbitmq_management, [
                  {listener, [
                      {port, 9001}
                  ]}
              ]}
          ].
          
***  
    sudo rabbitmq-plugins enable rabbitmq_management
    
    service rabbitmq-server start
    
    sudo rabbitmqctl add_user admin admin
    
    sudo rabbitmqctl set_user_tags admin administrator
    
    sudo rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"

***
    vi /etc/rabbitmq/rabbitmq.config -> to enable rabbitmq_prometheus

        [
            {rabbitmq_management, [
                {listener, [
                    {port, 9001}
                ]}
            ]}
        ].

## Rabbitmq prometheus start
    rabbitmq-plugins enable rabbitmq_prometheus
    
    rabbitmq-plugins enable rabbitmq_prometheus --offline
  
    port for rabbitmq -> 15692
  
    service rabbitmq-server restart

## DashBoard link

  https://grafana.com/grafana/dashboards/10991  -> Rabbitmq dashboard
