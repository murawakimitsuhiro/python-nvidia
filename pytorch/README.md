
## Build
`docker build ./ --build-arg PASSWORD=hogehoge -t pytorch`

## Run 
```
docker run --gpus all \
--rm \
-v /home/mrwk/.ssh:/tmp/.ssh \
-p 8022:22 \
--shm-size=4gb \
-itd pytorch
```
