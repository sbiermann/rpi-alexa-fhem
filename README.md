# rpi-alexa-fhem
Docker Image for Alexa-FHEM

# Build docker image
* clone this repository
* add alexa-fhem-0.1.9.tgz from https://forum.fhem.de/index.php/topic,60244.msg540117.html#msg540117
* run docker build .

# Run docker image
1. create directory /home/pi/alexa-docker-config
2. create config.json 
   ```json
{
    "alexa": {
        "name": "Alexa TEST",
        "keyFile": "./key.pem",
        "certFile": "./cert.pem",
        "nat-pmp": "",
        "nat-upnp": false,
        "applicationId": "amzn1.ask.skill.XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
        "oauthClientID": "amzn1.application-oa2-client.XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
    },
    
    "connections": [
        {
            "name": "FHEM",
            "server": "10.0.1.21",
            "port": "8083",
            "filter": "room=alexa"
        }
    ]
}
``` 
3. replace values in config.json with your values.
4. run in /home/pi/alexa-docker-config
   ```
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365
openssl rsa -in key.pem -out newkey.pem && mv newkey.pem key.pem
   ```
5. docker run -d --name alexa -p 3000:3000 -v /home/pi/alexa-docker-config/:/config sbiermann/rpi-alexa-fhem

