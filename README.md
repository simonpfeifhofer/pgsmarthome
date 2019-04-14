# PG Smart Home

PG Smart Home documents Alexa Voice Control integration in an existing Smart Home where:
- a Loxone-Mini-Server 
- a Raspberry-Pi and
- at least one Alexa
is in place for automation.

## Steps

1. Install Docker on a raspberry

   ```
   // Install
   curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh
   ```

2. Get and start HA-Bridge

  ```
  // Get image and start container
  docker run --name bridge -d --net=host -v /bridge/data/:/bridge/data -e PORT="-Dserver.port=8080" -e KEY="-Dsecurity.key=Xfawer3rspertSdf321234asd" michaelmiklis/rpi-habridge --restart always
  ```

3. Import Loxone Settings
   
   ```
   // clone importer (added as submodule)
   git clone https://github.com/escalate/loxone-ha-bridge-importer

   // import
   cd loxone-ha-bridge-importer
   ./importer.py --loxone-miniserver 192.168.188.36:1 --loxone-username <loxone-user> --loxone-password <loxone-pwd> --ha-bridge-server <raspberry-home-ip> --ha-bridge-port 8080 <raspberry-home-ip>

   // Make manualy adjustments in home-bridge
   http://<user-loxone>:<pwd-loxone>@<loxone-ip>:<loxone-port>/data/LoxAPP3.json returns you the configuration.

   ```
