# SMS Server Tools 3

The SMS Server Tools 3 is a SMS Gateway software which can send and receive short messages through GSM modems and mobile phones.

You can send short messages by simply storing text files into a special spool directory. The program monitors this directory and sends new files automatically. It also stores received short messages into another directory as text files. Binary messages (including Unicode text) are also supported, for example ring tone messages. It's also possible to send a WAP Push message to the WAP / MMS capable mobile phone.

http://smstools3.kekekasvi.com

## docker-compose.yml

```yml
version: '2'

services:
  smsd:
    image: 3apaxicom/smstools3
    restart: unless-stopped
    devices:
    # Your modem
      - /dev/ttyUSB1:/dev/ttyUSB1
    volumes:
      # config file
      - ./smsd.conf:/etc/smsd.conf
      # make folders before: mkdir -p spool/sms/sent spool/sms/failed spool/sms/checked spool/sms/outgoing spool/sms/incoming
      - ./spool/sms:/var/spool/sms
```

## Prepare

```sh
mkdir -p spool/sms/sent spool/sms/failed spool/sms/checked spool/sms/outgoing spool/sms/incoming

### Stop (and disable if you want)
```sh
sudo service ModemManager stop
sudo systemctl disable ModemManager
```

## Run
```sh
docker-compose up -d
```
