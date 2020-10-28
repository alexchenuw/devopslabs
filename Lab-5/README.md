## Lab 5. Build a customized NGINX Docker image with Dockerfile
___
This lab will create a customized docker image based on a Dockerfile. This image will host a webserver wtih a customized webpage that includes your first name.

* Create a folder called "mywebpage".

```bash
mkdir mywebpage
cd mywebpage
```

* Within the directory "mywebpage" create a local file called index.html with your first name in the content, replace "XXX" with your first name.

```bash
echo "This is XXX's web server" > index.html
```

* In the same directory create a Dockerfile with the contents listed below.  These commands will build an image from the NGINX base image and replace the default index.html file with the file you just created.

>Note: The Dockerfile should literally be called **Dockerfile**

```
FROM nginx
COPY index.html /usr/share/nginx/html/index.html
```

* Now build the customized image with docker build command

```bash
docker build . -t mywebpage
```

* Create a container based on the your new image.  Check the content of the default webpage using "curl" to ensure it includes your first name.  You should see "This is {firstname}'s web server" as the output from your webserver.

```bash
docker run -d -p 8788:80 mywebpage
curl http://localhost:8788/
```
Next try to reach your webserver using the public IP address associated to your linux. 

>Note: Also test your new webserver using a browser

```bash
export MYIP=`curl ifconfig.io`
curl http://${MYIP}:8788
```

Lab complete
___


