# docker-static-roots-nginx-recompile

Docker Hub link: https://hub.docker.com/r/asbelozerov/docker-static-roots-nginx-recompile/

Static site container: builds site from src with Roots (http://roots.cx), exposes site with Nginx.
Recompiles on server restart

#### Usage

Put your site source code including package.json to `/temp/src`  
Example Dockerfile:

    FROM asbelozerov/docker-static-roots-nginx
    COPY . /temp/src

To avoid compiling after server is running you can make pre-compilation  
Example Dockerfile:

    FROM asbelozerov/docker-static-roots-nginx
    COPY . /temp/src
    WORKDIR /temp/src
    RUN npm install && roots 
    RUN rm -rf /usr/share/nginx/html/
    RUN cp -r public/ /usr/share/nginx/html/
