# react typescript
Make react project with react-create-app 

$ npx create-react-app my-app –typescript 

When you use typescript, you need to add @types module. 

Success! Created my-app at 
Inside that directory, you 
npm start 
Starts the development 
npm run build 
/Users/be11 a/workspace/neural bc/my- app 
can run several commands: 
server. 
Bundles the app into static files for production. 
npm test 
Starts the test runner. 
npm run eject 
Removes this tool and copies build dependencies, configuration files 
and scripts into the app directory. If you do this, you can't go back! 
We suggest that you begin by typing: 
cd my-app 
npm Start 
Happy hacking! 
 

 
If you want to use scss then Install node-sass 

$ npm i node-sass 

$ npm i @types/node-sass -D 

 

Dockerizing(optional) 

Make Dockerfile and docker-compose.yml 

"scripts" : 
"start": " react—scripts start", 
"build . 
" react—scripts build", 
"test": " react-scripts test", 
"eject": " react—scripts eject", 
"docker:up": "docker—compose up —build" , 
"docker—prod:up": "docker-compose -f prod. docker-compose.yml up —build" , 
"docker:down": "docker—compose stop" , 
"docker—prod:down": "docker-compose -f prod. docker—compose. yml stop" 
 
Set tslint(optional) 

$ npm i tslint tslint-react tslint-config-airbnb typescript -D 

 
Router 

npm install -S react-router-dom 
 
npm install @types/react-router-dom –D 

 

Redux 

npm install redux react-redux immutable redux-actions 
 
npm install @types/react-redux @types/redux-actions -D 

 
Socket 

npm install socket.io-client 
 
npm install @types/socket.io-client -D