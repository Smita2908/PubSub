
# PubSub
Pub/Sub dockers with loadbalancer, two nchan-nodes and redis. Uses nchan, nginx and redis.

How to use the code?
1. Pull the respository.   
git clone https://github.com/Smita2908/PubSub.git   
docker pull redis
2. Build the docker images. 
docker build -t lb-nchan-redis/nchan-node nchan_node/  
docker build -t lb-nchan-redis/nginx-lb loadbalancer/  
3. Run the docker images 
docker run --detach --publish 3279:6379 --name=redis redis  
docker run --name=nchan-node1 -p 5000:80 -d lb-nchan-redis/nchan-node  
docker run --name=nchan-node2 -p 5001:80 -d lb-nchan-redis/nchan-node  
docker run -p 9070:80 -d --name=lbnginx lb-nchan-redis/nginx-lb  
4. You can establish websocket or http connection to //localhost:9070/pubsub/1
5. To see the access and error logs you can go inside docker to view error and access logs  
docker exec -it nchan-node1 sh
