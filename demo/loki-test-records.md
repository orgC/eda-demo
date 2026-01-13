
# records

cd /root/loki 
echo "$(date) ALERTME something bad happened" >> demo/app.log


curl -s -H "X-Scope-OrgID: fake" http://localhost:3100/prometheus/api/v1/rules  | jq .

curl -s -H "X-Scope-OrgID: fake" http://localhost:3100/prometheus/api/v1/alerts | jq .




