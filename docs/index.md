<h1 align="center">
  OpenVPN and Transmission with WebUI
</h1>

<p align="center">
  Docker container running Transmission torrent client with WebUI over an OpenVPN tunnel
  <br/><br/>

  <a href="https://hub.docker.com/r/tempestnano/transmission-openvpn/">
  </a>
</p>

## Quick Start

This container contains OpenVPN and Transmission with a configuration where Transmission is running only when OpenVPN has an active tunnel. It bundles configuration files for many popular VPN providers to make the setup easier.

You need to specify your provider and credentials with environment variables, as well as mounting volumes where the data should be stored. An example run command to get you going is provided below.

It also bundles an installation of Tinyproxy to also be able to proxy web traffic over your VPN, as well as scripts for opening a port for Transmission if you are using PIA or Perfect Privacy providers.

```
$ docker run --cap-add=NET_ADMIN -d \
              -v /your/storage/path/:/data \
              -v /etc/localtime:/etc/localtime:ro \
              -e CREATE_TUN_DEVICE=true \
              -e OPENVPN_PROVIDER=PIA \
              -e OPENVPN_CONFIG=CA\ Toronto \
              -e OPENVPN_USERNAME=user \
              -e OPENVPN_PASSWORD=pass \
              -e WEBPROXY_ENABLED=false \
              -e LOCAL_NETWORK=192.168.0.0/16 \
              --log-driver json-file \
              --log-opt max-size=10m \
              -p 9091:9091 \
              tempestnano/transmission-openvpn
```