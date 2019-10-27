# darkgate
### Simple tor|i2p proxy exposed as docker containers
This project is designed to quickly up the proxy server for access to the tor and i2p networks. 

1. Check out the repro and start a new proxy with

```
git cline https://github.com/ph20/darkgate.git
cd darkgate
docker-compose build # pay attention: this operation may take about 10-20 minutes
docker-compose up
```

2. Configure your browser to use http-proxy on port: 8118
```http://127.0.0.1:8118```


3. Shut down the proxy after usage with
```docker-compose down```


---
###### For creating this project was used such resources:
###### - https://github.com/hkparker/i2p-docker
###### - https://github.com/groundhog2k/torproxy
###### - https://github.com/danielguerra69/alpine-sdk
###### - https://github.com/danielguerra69/alpine-i2pd

---
### PAY ATTENTION
Project was created for study purpose only. 
The author is not responsible for the illegal use of this code. 
You use this code at your own risk.