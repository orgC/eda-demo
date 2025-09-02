

# 模拟 alertmanager 

## 触发 HighCPU → 执行 Remediate-CPU

```
WEBHOOK_URL="https://10.72.93.115/eda-event-streams/api/eda/v1/external_event_stream/5e4a01a5-075d-49be-8dfa-c6d34295b1ed/post/"

USERNAME=eda
PASSWORD=redhat2025

curl -k -sS -X POST "$WEBHOOK_URL" \
  -u "${USERNAME}:${PASSWORD}" \
  -H 'Content-Type: application/json' \
  -d '{
        "alert": {
          "labels": {
            "alertname": "HighCPU",
            "instance": "10.72.93.49",
            "severity": "critical",
            "host": "localhost"
          }
        }
      }'

```


## 触发 DiskFull → 执行 Remediate-Disk

```
curl -k -sS -X POST "$WEBHOOK_URL" \
  -u "${USERNAME}:${PASSWORD}" \
  -H 'Content-Type: application/json' \
  -d '{
        "alert": {
          "labels": {
            "alertname": "DiskFull",
            "instance": "vm-02",
            "severity": "warning",
            "host": "localhost"
          }
        }
      }'

```

## 触发未知告警 → 命中 catch-all（只打印日志）

```
curl -k -sS -X POST "$WEBHOOK_URL" \
  -u "${USERNAME}:${PASSWORD}" \
  -H 'Content-Type: application/json' \
  -d '{
        "alert": {
          "labels": {
            "alertname": "SomethingNew",
            "instance": "vm-03",
            "severity": "info",
            "host": "localhost"
          }
        }
      }'


```