
```
export KONG_LICENSE_DATA='datatatatatata'   

docker-compose up -d
```

>> These will be explained over call.




## Activity 1
> set Hash On = `cookie` , Healthchecks.Threshold , Healthchecks.Active.Unhealthy.Interval , Healthchecks.Active.Unhealthy.Tcp Failures. on upstream to ensure 


<img width="1004" alt="Screenshot 2022-09-21 at 4 33 41 AM" src="https://user-images.githubusercontent.com/1439169/191379943-43ff2f94-be08-496b-b6b9-dde5a0569cd8.png">
<img width="1006" alt="Screenshot 2022-09-21 at 4 33 35 AM" src="https://user-images.githubusercontent.com/1439169/191379946-237aaba4-9f19-4e24-8f22-3f07d328d1dc.png">

1.5 marking upstream as unhealhty from UI or cli
```
curl -X GET http://localhost:8001/upstreams/httpbin-upstream -H 'Kong-Admin-Token:password'
curl -i -X POST http://localhost:8001/upstreams/httpbin-upstream/targets/d43ffe0d-7fea-46de-8f66-d0601dbb0b46/unhealthy -H 'Kong-Admin-Token:password'
```


## Activity 2
```
curl -i -X POST http://localhost:8001/services/httpbin-service/plugins --data "name=key-auth" -H 'Kong-Admin-Token:password'

curl -i -X POST \
  --url http://localhost:8001/consumers/ \
  --data "username=u1" -H 'Kong-Admin-Token:password'


curl -i -X POST \
  --url http://localhost:8001/consumers/ \
  --data "username=u2" -H 'Kong-Admin-Token:password'


curl -i -X POST http://localhost:8001/consumers/u1/key-auth --data "" -H 'Kong-Admin-Token:password'

curl -s -X POST http://localhost:8001/consumers/u1/plugins --data "name=rate-limiting"  --data "config.hour=3" -H 'Kong-Admin-Token:password' | jq .
curl -s -X POST http://localhost:8001/consumers/u2/plugins --data "name=rate-limiting" --data "config.hour=5" -H 'Kong-Admin-Token:password' | jq .

curl -s -X GET http://localhost:8001/consumers/u1/plugins/  -H 'Kong-Admin-Token:password' | jq .
curl -s -X GET --url http://localhost:8000/echo  --header 'apikey: oIX3C0TM5AZZKNf6UPs1MXOEWRgHh310'  | jq .
curl -s -X DELETE http://localhost:8001/consumers/u1/plugins/3e725462-9f01-4ebb-a376-2c7ee8c9998f  -H 'Kong-Admin-Token:password' | jq .
```

## Activity 3
