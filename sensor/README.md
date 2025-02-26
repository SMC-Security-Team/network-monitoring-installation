# Network Monitoring Sensor
## รัน Sensor โดยใช้ Docker

สามารถรันโดยใช้ docker compose กับไฟล์ docker-compose.yml ตัวอย่างได้เลย
ซึ่งต้องมีการติดตั้ง Worker ก่อนเพื่อให้ Sensor ติดต่อไปได้

```
version: "3"

services:
  zeek:
    build:
      context: ./zeek
    environment:
      - INTERFACE=enp1s0 # <<<< Change this to your desired interface
    volumes:
      - ./logs/zeek:/logs
    network_mode: host
    cap_add:
      - NET_ADMIN

  suricata:
    build:
      context: ./suricata
    environment:
      - INTERFACE=enp1s0 # Change this to your desired interface
    volumes:
      - ./logs/suricata:/var/log/suricata
      - ./suricata/rules/custom.rules:/var/lib/suricata/rules/custom.rules
      - ./suricata/config/suricata.yaml:/etc/suricata/suricata.yaml
    network_mode: host
    cap_add:
      - NET_ADMIN
      - NET_RAW
      - SYS_NICE

  log-processor:
    build:
      context: ./log-processor
    ports:
      - "24224:24224"
    environment:
      - SERVER_URL=http://10.0.0.10:9090 # <<<< Worker API URL
      - AUTH_TOKEN=[KEY_FROM_WORKER_HERE] # <<<< Sensor's key from the worker
    network_mode: host

  fluent-bit:
    build:
      context: ./fluent-bit
    volumes:
      - ./logs/zeek:/zeek-logs:ro
      - ./logs/suricata:/suricata-logs:ro
    network_mode: host
    extra_hosts:
      - "log-processor:127.0.0.1"
    depends_on:
      - zeek
      - suricata
      - log-processor
```
