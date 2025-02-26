# การติดตั้ง Network Monitoring Worker
## รัน Worker โดยใช้ Docker
Environment Variables ที่จำเป็นต้องใช้
```
# Example
MYSQL_CONNECTION_STRING=root:root@tcp(10.0.0.30)/netsight?parseTime=true
OPENSEARCH_USERNAME=admin
OPENSEARCH_PASSWORD=password
MISP_ADDRESS=https://10.0.0.20 # MISP's IP Address
MISP_AUTHKEY=df8loZ2NoEjSM0JOEsGB7pej5dR0cp8sCO7uy4NG
```
