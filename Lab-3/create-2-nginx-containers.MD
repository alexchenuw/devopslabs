1, create the first container with command "docker run --name firstcontainer -d -p 5688:80 nginx"

2, create the second container with command "docker run --name secondcontainer -d -p 5699:80 nginx"

3, use "curl http://docker-host-ip:5688/" and "curl http://docker-host-ip:5699/" to see the webpage result

4, create first index1.html file with the content as: <center>This is container one web server </center>

5, create the second index2.html file with the content as: <center>This is container two webserver </center>

6, use docker cp to copy the index1.html file into the first and second container respectively: "docker cp index1.html firstcontainer:/usr/share/nginx/html/index.html"

7, use docker cp to copy the index2.html file into the first and second container respectively: "docker cp index2.html secondcontainer:/usr/share/nginx/html/index.html"

3, use "curl http://docker-host-ip:5688/" and "curl http://docker-host-ip:5699/" to see the webpage result again.
