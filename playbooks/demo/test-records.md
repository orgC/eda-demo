

# 模拟 alertmanager 

## 触发 HighCPU → 执行 Remediate-CPU

```
WEBHOOK_URL="https://<your-aap>/api/eda/v1/events/<token>"

curl -sS -X POST "$WEBHOOK_URL" \
  -u "${USERNAME}:${PASSWORD}" \
  -H 'Content-Type: application/json' \
  -d '{
        "alert": {
          "labels": {
            "alertname": "HighCPU",
            "instance": "vm-01",
            "severity": "critical",
            "host": "localhost"
          }
        }
      }'

```


## 触发 DiskFull → 执行 Remediate-Disk

```
curl -sS -X POST "$WEBHOOK_URL" \
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
curl -sS -X POST "$WEBHOOK_URL" \
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