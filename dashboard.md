# การติดตั้ง Network Monitoring Dashboard
* ไม่ใช่ Dashboard ที่มากับ OpenSearch หรือ Wazuh

# รัน Dashboard โดยใช้ Docker

Environment Variables ที่จำเป็นต้องใช้
```
# Example
MYSQL_CONNECTION_STRING=root:root@tcp(127.0.0.1)/netsight?parseTime=true
DASHBOARD_PASSWORD=password
DASHBOARD_USERNAME=admin
OPENSEARCH_ADDRESS=https://127.0.0.1:9200
OPENSEARCH_USERNAME=admin
OPENSEARCH_PASSWORD=password
PORT=9090
```
