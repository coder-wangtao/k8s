Filebeat：是 Elastic Stack 的一部分，主要负责轻量级日志收集。它会在目标服务器上运行，并将日志文件内容转发到 Logstash 或 Elasticsearch。
Logstash：是一个强大的数据处理管道，负责从多个来源（如 Filebeat、应用程序日志、数据库等）收集、过滤、解析、转发日志或数据。它通常用于处理复杂的日志解析和转换工作。
Elasticsearch：用于存储和索引日志数据，方便后续的查询和分析。
Kibana：用于日志数据的可视化，提供交互式仪表板。

1.安装 Filebeat
2.Filebeat 的配置文件通常位于 /etc/filebeat/filebeat.yml。你需要在这个文件中指定 日志路径 和 Logstash 的地址。

<!--
filebeat.inputs:
- type: log
  enabled: true
  paths:
  - /var/log/\*.log # 配置你需要收集的日志路径
output.logstash:
hosts: ["logstash-server:5044"] # Logstash 服务器地址和端口
-->

3.安装 Logstash

4.配置 Logstash。Logstash 的配置文件通常位于 /etc/logstash/conf.d/ 目录中。你需要在这个目录下创建一个 .conf 文件。

<!--
input {
  beats {
    port => 5044
  }
}

filter {
  # 对日志进行解析和过滤（可以根据实际需求来定义）
  grok {
    match => { "message" => "%{COMMONAPACHELOG}" }  # 使用 Grok 进行日志解析
  }
}

output {
  elasticsearch {
    hosts => ["http://elasticsearch-server:9200"]
    index => "logs-%{+YYYY.MM.dd}"  # 将日志输出到 Elasticsearch，按日期创建索引
  }
  stdout { codec => rubydebug }  # 输出到控制台，方便调试
}
-->

5. 查看 Elasticsearch 和 Kibana
   如果你的 Logstash 配置已经正确地输出到 Elasticsearch，你可以通过 Kibana 来查看日志数据。
   登录到 Kibana（通常是 http://<kibana-server>:5601）。
   配置索引模式（Index Pattern）为 logs-\*。
   浏览 Discover，查看收集的日志数据。

6.流程
Filebeat (日志收集)
↓
Logstash (日志处理、过滤、解析)
↓
Elasticsearch (日志存储和索引)
↓
Kibana (可视化、分析日志)
