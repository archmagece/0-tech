# websocket

https://medium.com/bigpanda-engineering/load-testing-web-sockets-2c5a499e447e

## artillery
https://artillery.io/
npm install -g artillery 
artillery quick — count 1 -n 1 ws://localhost:3000

## thor
https://github.com/observing/thor
npm install -g thor
thor --amount 5 ws://localhost:3000

## websocket-bench
https://github.com/M6Web/websocket-bench
npm install -g websocket-bench
websocket-bench -a 1 -c 1 -t primus -p engine.io -v -w 1 -n /web/primus ws://localhost:3000

