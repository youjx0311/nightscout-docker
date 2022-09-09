# nightscout-docker
Nightscout docker with remote overrides and loop support for ARM64 v8 including Raspberry Pi 4 and Xiaomi router AX9000

## Credit
I update the docker-compose.yml file form pyrmon/nightscout-docker. Thank you!

## Requirements for this to work

* Any sort of Linux Computer/Server, have tested it both on ARM processors and AMD processors
* Docker and Docker-Compose installed (google it if you don't know how to do that)
* Administrative access to your router

## Setup Nightscout

* I have included the Dockerfile that I used, but it is for refrence only
* First Clone this repository to your server and go into the folder
```sh
git clone https://github.com/florianschi909/nightscout-docker && cd nightscout-docker
```
* Edit the docker-compose-amd.yml file
    * Change the API_SECRET value to a password with the min length of 12, I don't know if all special characters are okay
    * Change the BASE_URL to the webadress you want to access Nightscout from later on 
        * if you don't know this yet then wait for my instructions (which I will write later) where I tell you how you can get a free domain
    * Change the LOOP_APNS_KEY value to the ENTIRE contents of your downloaded Apple .p8 file including the BEGIN and END lines.
    * Change the LOOP_APNS_KEY_ID to the string of characters on the .p8 download file immediately following the underscore ( _ ) and not including the file extension ( .p8 ), or you can get it from your saved key in your developer account.
    * Change the LOOP_DEVELOPER_TEAM_ID value to the string where you get from Loop app signing or in your developer account's top right corner under your name.
    * If you don't use mmol/L then you can change DISPLAY_UNITS value to mg/dl
```Dockerfile
      # admin secret
      - API_SECRET=xxxxxxxxxxxx
      # the URL to this Nightscout instance
      - BASE_URL=https://ns.xxxxx.com
      # The content of your Apple p8 key file.
      - LOOP_APNS_KEY=xxxxxxxxxxxx
      # The ID of your Apple p8 key.
      - LOOP_APNS_KEY_ID=xxxxxxxxxxxx
      # The team ID of your apple developer account.
      - LOOP_DEVELOPER_TEAM_ID=xxxxxxxxxxxx
      ...
      # use SI units by default
      - DISPLAY_UNITS=mmol/L
```
* This is it. Now follow this command and your Nightscout is running on the webadress http://localhost:1337/
```sh
docker-compose up -d
```

## Setup Nginx

* This will only be the explanation on how to get Nginx running
* How the ssl certificate creation and proxy hosts work I will explain in a later commit
* Just enter these commands and it will setup Nginx Proxy Mangager on http://localhost:81
```sh
cd nginx
docker-compose -f docker-compose-nginx.yml up -d
```
* After this you can sign in as admin@example.com with the password changeme
