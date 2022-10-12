# Source code
http://devops.edunmore.de:8082/assets/app.zip


# GitHub Repo (wiord beim Manuellen nicht gebraucht)

Source code laden
wget http://devops.edunmore.de:8082/assets/app.zip

# Entpacken mit mc (midnight commander) # apt install mc

# Dockerfile anlegen und aus dem Beispiel kopieren

FROM node:12-alpine
# Adding build tools to make yarn install work on Apple silicon / arm64 machines
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]

# in index.js den Port auf 80 ändern
# Zeile 18 3000->80
    app.listen(80, () => console.log('Listening on port 80'));

# image bauen
# -t name des Images - muss eindeutig auf dem Rechner sein!!!
in das Verzeichnis wechseln, indem auch das Dockerfile ist
cd ./app
docker build -t cicduebungmarcus .

# testen, ob das image da ist
docker images |grep cicd

# image mal zum testen als tar laden (mit mc anschauen)
docker save cicduebungmarcus > cicduebungmarcus.tar

# mal runnen (ohne -d)
docker run -p 8083:80 --name cicduebungmarcus --rm cicduebungmarcus 

# mal -d im Hintergrund
docker run -d -p 8083:80 --name cicduebungmarcus --rm cicduebungmarcus 
# log anschauen
docker logs cicduebungmarcus
docker stop cicduebungmarcus
docker ps |grep cicd

# image auf docker hub laden

# image über godeploy in Azure über das Portal als Webapp starten

# image über godeploy in Azure über die Azure CLI starten (az ...)

