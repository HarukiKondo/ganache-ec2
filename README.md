# Playground Ganache su AWS EC2 & Docker
Ambiente simulato di una blockchain Ethereum via Ganache. Questa repository è un playground per un progetto universitario che ha il fine di deployare la rete su EC2, containerizzarla con Docker e renderla fruibile via Node.

## .env
`BLOCKCHAIN_IP_ADDRESS` deve puntare all'IP pubblico dell'istanza di EC2, definita all'avvio dell'istanza EC2.

# Istruzioni per l'uso

0. Connessione SSH su EC2
    - `cd ~/ganache-ec2-root-path`
    - `chmod 400 [key].pem`
    - ssh -i "ganache-ec2.pem" ubuntu@ec2-3-71-206-133.eu-central-1.compute.amazonaws.com
1. Creazione istanza EC2 
    - `t2.micro`
        - Intel Xeon (3,3 GHz)
        - 1 vCPU, 1 GB RAM
    - `Ubuntu 20.04 LTS`
    - `Security Group` con le seguenti regole:
        - `SSH (:22)`
        - `HTTP (:80)`
        - `Custom TCP Route [Web3] (:8545)`
2. Installare Node CLI e il Package Manager `nvm`
3. Installare `ganache-cli` via `npm -g`
4. Avviare la simulazione (_docker-less_) 
    - `ganache-cli --host "[EC2 Private IPv4]"  --port 8545 --networkId 5777`
5. **Unto Docker:** [Installazione di Docker su EC2](https://dev.to/nazmifeeroz/build-your-own-remote-private-blockchain-with-aws-and-ganache-part-2-2cie)
6. Creazione del container di Ganache su EC2 (`~/ganache-ec2`)
    - `sudo docker build -t ganache .`
    - `sudo docker run -d -p 8545:8545 ganache`
    - `sudo docker logs {GANACHE_CONTAINER_ID / sudo docker ps}`
7. Parametrizzare l'IP *pubblico* dell'istanza EC2 all'interno del file `.env`
8. Avviare la comunicazione via `yarn && yarn start` (_docker-less_)
