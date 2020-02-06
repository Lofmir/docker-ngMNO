# docker-ngMNO
Docker-based end-to-end LTE network (NextEPC + srsLTE) with the USRP drivers from the Ettus Research PPA.
Fork from https://github.com/ravens/docker-nextepc with modifications for USRP support.
Featuring NextEPC as MME, SGW, PGW and PCRF. From srsLTE the srseNB will be used. 

## setup 

```
docker-compose build --no-cache
```

## running

We just need to run the docker-compose:
```
docker-compose up -d
```

The following service should be running:
```
docker-compose ps
 Name                Command               State           Ports
-------------------------------------------------------------------------
enb       stdbuf -o L srsenb /config ...   Up
hss       /bin/sh /etc/nextepc/run_h ...   Up
mme       /bin/sh /etc/nextepc/run_m ...   Up
mongodb   docker-entrypoint.sh mongod      Up      27017/tcp
pcrf      /bin/sh /etc/nextepc/run_p ...   Up
pgw       /bin/sh /etc/nextepc/run_p ...   Up
sgw       /bin/sh /etc/nextepc/run_s ...   Up
ue        stdbuf -o L srsue /config/ ...   Up
webui     npm run start --prefix /ne ...   Up      0.0.0.0:3000->3000/tcp
```

After a while this should settle done and you should see the following kind of output :
```
ue               | Found PLMN:  Id=00101, TAC=1
ue               | Random Access Transmission: seq=46, ra-rnti=0x2
enb              | RACH:  tti=631, preamble=46, offset=0, temp_crnti=0x46
ue               | RRC Connected
ue               | Random Access Complete.     c-rnti=0x46, ta=0
sgw              | 05/25 22:42:54.275: [gtp] INFO: gtp_connect() [192.168.26.20]:2123 (gtp_path.c:77)
sgw              | 05/25 22:42:54.275: [gtp] INFO: gtp_connect() [192.168.26.40]:2123 (gtp_path.c:77)
pgw              | 05/25 22:42:54.276: [gtp] INFO: gtp_connect() [192.168.26.30]:2123 (gtp_path.c:77)
pgw              | 05/25 22:42:54.276: [pgw] INFO: UE IMSI:[001010000000001] APN:[internet] IPv4:[45.45.0.2] IPv6:[] (pgw_context.c:922)
pgw              | 05/25 22:42:54.276: [gtp] INFO: gtp_connect() [192.168.26.30]:2152 (gtp_path.c:77)
sgw              | 05/25 22:42:54.279: [gtp] INFO: gtp_connect() [192.168.26.40]:2152 (gtp_path.c:77)
ue               | Network attach successful. IP: 45.45.0.2
enb              | User 0x46 connected
pgw              | 05/25 22:42:54.276: [gtp] INFO: gtp_connect() [192.168.26.30]:2123 (gtp_path.c:77)
pgw              | 05/25 22:42:54.276: [pgw] INFO: UE IMSI:[001010000000001] APN:[internet] IPv4:[45.45.0.2] IPv6:[] (pgw_context.c:922)
pgw              | 05/25 22:42:54.276: [gtp] INFO: gtp_connect() [192.168.26.30]:2152 (gtp_path.c:77)
sgw              | 05/25 22:42:54.275: [gtp] INFO: gtp_connect() [192.168.26.20]:2123 (gtp_path.c:77)
sgw              | 05/25 22:42:54.275: [gtp] INFO: gtp_connect() [192.168.26.40]:2123 (gtp_path.c:77)
sgw              | 05/25 22:42:54.279: [gtp] INFO: gtp_connect() [192.168.26.40]:2152 (gtp_path.c:77)
sgw              | 05/25 22:42:54.523: [gtp] INFO: gtp_connect() [192.168.26.60]:2152 (gtp_path.c:77)
ue               | (t
ue               | ! 25/5/2019 22:42:54 TZ:0
sgw              | 05/25 22:42:54.523: [gtp] INFO: gtp_connect() [192.168.26.60]:2152 (gtp_path.c:77)
```
