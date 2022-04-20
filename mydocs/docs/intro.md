---
sidebar_position: 1
---

# site static: Docusaurus 

# Démarrage

générer les premières pages sans installer nodejs sur son poste, oui c'est possible avec docker : 

```bash 
cd PROJECT_DIR 
docker run -it --rm --entrypoint=/bin/bash -u 1000 -v $PWD:/data -p 3000:3000 node:lts
node@d601786e5765:/$ id 
uid=1000(node) gid=1000(node) groups=1000(node)
node@d601786e5765:/$ cd data/
node@d601786e5765:/data$ npx create-docusaurus@latest mydocs classic
Need to install the following packages:                                                              
  create-docusaurus@latest
Ok to proceed? (y) y
[INFO] Creating new Docusaurus project...
[INFO] Installing dependencies with npm...
.....
[SUCCESS] Created mydocs.
node@d601786e5765:/data$ cd mydocs/
node@d601786e5765:/data/mydocs$ npx docusaurus start --host 0.0.0.0
[INFO] Starting the development server...
[SUCCESS] Docusaurus website is running at http://localhost:3000/.

✔ Client
  Compiled successfully in 8.07s

client (webpack 5.72.0) compiled successfully
^C
node@d601786e5765:/data/mydocs$ exit
tree -L 2
.
└── mydocs
    ├── babel.config.js
    ├── blog
    ├── docs
    ├── docusaurus.config.js
    ├── node_modules
    ├── package.json
    ├── package-lock.json
    ├── README.md
    ├── sidebars.js
    ├── src
    └── static
```

# Dockerfile dev / prod 

ref : https://dev.to/cindyledev/how-to-dockerize-a-docusaurus-v2-application-fp7

avec le Dockerfile présent à la racine : 

## travail en environnement de dev 

```
docker build --target developpement -t docs:dev .
docker run -p 3000:3000 docs:dev
```

## lancement de la production 

```
docker build -t docusaurus:latest .
docker run --rm -p 3000:80 docusaurus:latest
```

