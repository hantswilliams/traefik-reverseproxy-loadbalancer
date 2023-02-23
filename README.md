# About 

- this is a working version of using TRAEFIK as a reverse proxy/load balancer on Machine A - and then having a number of other different services (say Flask applications on Machine B, C, D) being routed via Traefik 

- in order for this to work, need to have the Traefik's IP address mapped to the main/root domain - a record - within your DNS managmenet service (e.g., godaddy, aws, etc...)

- for each additional subdomain, all you need to do is create a new A-record, and then have the IP address for that subdomain point to the Traefik IP address, and it will handle the rest 

- what i still need to test here is doing the DNS authentication - that way can have the Traefik service automatically generate the appropriate A-records that point back to the root IP - this would save some time, but not necessary for load balancing purposes, only impact reverse proxy 

## Instructions 
- Create 4 servers - and install docker, docker-compose on each of them
- Document their IP addresses / make sure port 80 and 443 is open on each, in addition should add port 8080 for the server that will contain and run the reverse proxy/load balancer Traefik 
    1. The first server should act as the reverse proxy/load balancer where you copy this repo and then just run the docker-compose file here at the root folder level, which will get traefik up and running. Before you run the docker-compose command, be sure to: 
        - Update the DNS record so there is a root main record that points to the Traefik IP address 
        - Update the different servers with your own IP address for the different flask applications within the `traefik.yaml` file 
    2. Then servers 2-4 will be the different applications 
        - The way I have this setup right now, is that server 2 is the main root domain, server 3 is a app1.domain and server 4 is a app2.domain 
        - this way we are mimickign real work -> e.g., expect to have different applications running on different servers and not all sharing the same server 