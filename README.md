# Docker ELK installation (Server)

<code>
git clone https://github.com/thuannvn/ELK-docker-filebeat-Centralized-Log-System.git
cd ELK-docker-*
docker-compose up
</code>

Then access GUI http://host-ip:5601/ & create button (replace logstash-* with *)

# Install FileBeat (Client)

https://www.elastic.co/downloads/beats/filebeat

# How it works

Client will send logs to server through logstash (server configure accept logstash INPUT)

# Server logstach config

vi logstash/config/logstash.conf
input {
   beats {
     type => beats
     port => 5000
   }
}

output {
        elasticsearch {
                hosts => "elasticsearch:9200"
        }
}

# Client filebeat config (Remember to remove elasticsearch output, replace with logstash)

vi /etc/filebeat/filebeat.yml
logstash:
     hosts: ["172.16.20.113:5000"]
