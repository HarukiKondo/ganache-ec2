# Ganache su AWS EC2 & Docker
Ambiente simulato di una blockchain Ethereum via Ganache. Questa repository è un playground per un progetto universitario che ha il fine di deployare la rete su EC2, containerizzarla con Docker e renderla fruibile via Node.

### .env
`BLOCKCHAIN_IP_ADDRESS` deve puntare all'IP pubblico dell'istanza di EC2, definita all'avvio dell'istanza EC2.

![arch](https://i.gyazo.com/9f9c2ec5c8b4f297f4fb1793ab9340fc.png)

# Creazione ed utilizzo dell'istanza

0. Connessione SSH su EC2
    - `cd ~/ganache-ec2`
    - `chmod 400 ganache-ec2.pem`
    - `ssh -i "ganache-ec2.pem" ubuntu@ec2-3-71-12-237.eu-central-1.compute.amazonaws.com`
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
4. Avvio _docker-less_ della simulazione 
    - `ganache-cli --host "[EC2 Private IPv4]"  --port 8545 --networkId 5777`
5. **Unto Docker:** [Installazione di Docker su EC2](https://dev.to/nazmifeeroz/build-your-own-remote-private-blockchain-with-aws-and-ganache-part-2-2cie)
6. `git clone https://github.com/antoniogrv/ganache-ec2.git`
7. Creazione del container di Ganache su EC2 (`~/ganache-ec2`)
    - `sudo docker build -t ganache .`
    - `sudo docker run -d -p 8545:8545 ganache`
        - Avvio _docker-ful_ della simulazione
    - `sudo docker logs {GANACHE_CONTAINER_ID / sudo docker ps}`
8. Parametrizzare l'IP *pubblico* dell'istanza EC2 all'interno del file `.env`
9. Avviare la comunicazione in locale (`git bash`) via `yarn && yarn start`
