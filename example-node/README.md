## Example of app on node js with Hapi

#### Quick start
```bash
# building image from dockerfile
sudo docker build -t nodetest .

# check images
sudo docker images

# runnig image
sudo docker run -d -P nodetest
# -d - detach from console
# -P - make random port for app outside

# check container 
sudo docker ps 

# check logs
sudo docker logs [container-id]

# make request 
curl -i localhost:[your-port from docker ps]

# OR if windows
curl -i 192.168.99.100:[your-port from docker ps]

```
