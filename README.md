# Dockerwebserver

### Agenda
Main Agenda of this assignment is learn basics of Docker with a simple html page,configuring ngnix,creating docker image and pushing the image into ecr.
### Requirements of project
install docker into machine

```
sudo apt install docker.io -y
```
```
Check the docker running status

sudo systemctl status docker

```
1. create HTML Page:

```
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello, Docker!</title>
</head>
<body>
    <h1>Hello, Docker!</h1>
</body>
</html>

```
2. Next Nginx Configuration:

   - Create an Nginx configuration file named `nginx.conf` that serves the `index.html` page.

   - Configure Nginx to listen on port 80.
```
events {}
http {
    server {
        listen 80;
        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
}
```
3. Next Dockerfile:

   - Create a `Dockerfile` to define the Docker image.

   - Use an official Nginx base image.

   - Copy the `index.html` and `nginx.conf` files into the appropriate location in the container.

   - Ensure that the Nginx server is started when the container is run.
```
# Dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

```
4. Buil the Docker Image:
   - Build the Docker image using the `Dockerfile`.
     ```
     sudo docker build -t custom_webserverakhil:v1 -f Dockerfile .
     ```

 5.Test the image

 ```
 docker run -it -d  -p 8080:80 custom_webserverakhil:v1
 ```

6. Push the image to ECR

   - Make the public repository in ECR and push them on to the ECR
  
    ```
     sudo docker tag custom_webserverakhil:v1 public.ecr.aws/c3w1m1q2/dockerwebserverakhil:latest
     sudo docker push public.ecr.aws/c3w1m1q2/dockerwebserverakhil:latest
    ```
    ## Please Find below the screenshot of all above steps![Screenshot (2610)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/9fc307c4-87c8-4ba0-a030-4b7e9bb7e6f2)
![Screenshot (2609)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/5a9339d2-edd1-45f3-9924-254abc009c61)
![Screenshot (2608)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/bf48f862-cd94-40cb-a3b1-35ebfcbd1f6d)
![Screenshot (2607)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/6705be7a-25af-40b7-b497-64628cfdfe18)
![Screenshot (2606)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/f15a9baf-a9e2-4a17-afcc-5d6fc0745683)
![Screenshot (2605)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/b8ca9c7f-cb0f-49f8-a246-9e3ea12ba8cb)
![Screenshot (2604)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/38a2829a-97e0-4832-8016-995bb0313ab6)
![Screenshot (2602)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/f128ad31-ce98-466b-94e8-f744e08a59d0)
![Screenshot (2601)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/f507a1d3-8c84-4bca-9c80-793e1aecc713)
![Screenshot (2599)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/093aa3ff-b4d4-4ec3-974e-e7bef8f7c6f9)
![Screenshot (2598)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/b589b614-c390-41ef-a550-440542f88491)
![Screenshot (2597)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/6d374048-825c-4bba-9fef-0c35219659c7)
![Screenshot (2596)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/9ec44127-a43b-43e0-8940-6db231dc2c1c)
![Screenshot (2595)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/0d0731bd-9f7f-46d6-98f3-fb04992729fc)
![Screenshot (2594)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/f97265cd-ac52-442e-88b9-430b9ac729cb)
![Screenshot (2593)](https://github.com/Akhilbmsb/Dockerwebserver/assets/54345937/9dc4def5-ec60-498b-897c-9343aac65187)


