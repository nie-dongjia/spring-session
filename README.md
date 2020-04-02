spring-session多节点

nohup java -jar spring-session-web-1.0-SNAPSHOT.jar --server.port=9601 &

nohup java -jar spring-session-web-1.0-SNAPSHOT.jar --server.port=9602 &


## nginx 配置 
1、配置集群 
upstream spring-boot-session {
  server localhost:9601;
  server localhost:9602;
}
location /spring-session-web {
    proxy_pass http://spring-boot-session/spring-session-web/;
    access_log on;
          proxy_redirect off;
} 
2、重启nginx 
/usr/local/nginx/sbin/nginx -s reload     

3、启动多节点服务 
nohup java -jar spring-session-web-1.0-SNAPSHOT.jar --server.port=9601 &
nohup java -jar spring-session-web-1.0-SNAPSHOT.jar --server.port=9602 &

4、测试是否成功 

