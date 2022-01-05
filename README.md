# DockerCLI
## Comandos de docker
- Ejecucion de la instancia de una imagen
- Docker is an open containerzation engine

docker images : ver imagenes
docker run hello-world
 
docker search ubuntu buscar imagenes

## RUN CONTAINERS
run ubuntu echo 'hola mundo'
docker run --name name_i_want hello-world



## VIEW CONTAINER PROCESSES
ps -a (all)          			historial
docker ps -aq :				muesta los id de los contenedores
docker inspect <ID or name_container> :	show config container

## STOP AND START PROCESS
docker start  #
docker stop #

## DELETE CONTAINER
docker rm <ID o nombre> (borro un contenedor)
docker rm  $(sudo docker ps -aq) elimina cada id, pasamos como parametro la lista de los id`s

docker rm $(sudo docker ps -aq) -f para forzar pararlo y eliminarlo
docker container prune (borro todos lo contenedores que esten parados)

## MODO INTERACTIVO
~ docker run -it ubuntu bash  :     -it: interactiva,  comando: bash
~ docker run it debian  


~ docker pull ngxi	x: descargar la imagen de nginx

~docker run nginx
~docker run -p 3000:80 nginx
~docker run -p 3000:80 -d nginx : la -d signigica detach para que se ejecute en segundo plano

~docker run --memory="100m" --cpus=0.5 <image>
puerto 3000 :mi maquina  80:contenedor
sudo docker run   -p 3000:80 -p 4000:80 -p 5000:80 -d nginx 

SALIDA PERSONALIZADA : sudo docker ps --format="ID\t{{.ID}}"
docker ps --format="ID\t{{.ID}}\nNombre:\t{{.Names}}"


sudo docker ps --format="$DOCKER_FORMAT" : le pasamos la variable de entorno

sudo kill -9 "$(sudo docker inspect --format '{{.State.Pid}}' alwaysup)" matar proceso 

docker run httpd

Ejecucion de la instancia de una imagen 

Docker is an open source containerzation engine


--COPIAR ARCHIVOS ( Al CONTENEDOT) CON NGINX
docker run -d -p 3000:80  --name webstite -v $(pwd):/usr/share/ngix/html nginx

~ docker run --name alwaysup -d ubuntu tail -f /dev/null

--EJECUTAR BASH  en el contenedor
docker exec -it website bash
docker exec : nos permite ejecutar un comando o un proceso

~ docker kill name_container

CREAR MI PROPIA IMAGEN 

Dockerfile: ESTO ES UN PASO A PASO PARA PASAR A OTRA PERSONA
1. paso crear el archivo Dockerfile y pegar esto

DOCKER FILE
FROM nginx:1.19.6
FROM nginx:latest

WORKDITR /usr/share/nginx/html

2. paso crear mi propia imagen desde el Dockerfile -t para darle un nombre a la imagen

docker build  -t imagendiego .

3. para correr el contenedor con mi imagen creada (diegoimagen) y le damos nombre al contenedor (--name)

docker run -p 4000:80 -d --name diegoapp  imagendiego

## Bind Mount
~ docker run --name  db mongo
~ docker ps
~ docker exec -it db bash
#Shell
 mongo: binario que viene con mongo
 db.users.insert({"nombre": diego})

~ docker logs db
