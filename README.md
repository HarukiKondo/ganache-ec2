# Ganache: AWS/Docker
Ambiente simulato di una blockchain Ethereum via Ganache. Questa repository è un playground per un progetto universitario che ha il fine di deployare la rete su EC2 e containerizzarla con Docker.

## .env
`BLOCKCHAIN_IP_ADDRESS` deve puntare all'IP pubblico dell'istanza di EC2, definita all'avvio della simulazione.

# Running
### Over EC2 on FS
```
yarn && yarn start
```

### Over EC2 on Docker

```
sudo docker build -t ganache .
sudo docker run -d -p 8545:8545 ganache
sudo docker logs {GANACHE_CONTAINER} [over docker ps]
```
