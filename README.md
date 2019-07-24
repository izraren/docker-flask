# Pull code 

git clone https://github.com/izraren/docker-flask

cd flask-docker

# Create docker registry

docker run -d -p 5000:5000 --restart always --name registry registry:2

# Build Docker Image

docker build -t flask-demo:latest .

# Push Image to docker registry

docker tag flask-demo:latest localhost:5000/flask-demo:latest

docker push localhost:5000/flask-demo:latest

# Start Flask Container

docker run -d -p 80:80 --name flask1 localhost:5000/flask-demo:latest

# Change code
   Entre en mode bash sur docker:  docker exec -it < d container> bash
   
   Edit votre fichier app.py: vim app.py 
        #(si vim n'est pas installer taper en mode bash toujoures ces commandes: apt-get update puis apt-get install vim)
        
   Exit mode bash: ctrl +d
   
# rebuild and push image to registry

docker build -t flask-demo:latest

docker tag flask-demo:latest localhost:5000/flask-demo:latest

# Redeploy

docker rm -f flask1

docker run -d -p 80:80 --name flask1 flask-demo
