
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list
sudo apt-get update

sudo apt-get install mongodb-org
sudo service mongod start


sudo apt-get install nodejs
#sudo apt-get install npm

cp /usr/bin/nodejs /usr/bin/node

nano ~/.tunecore/tune.conf
  rpcuser=user
  rpcpassword=password
  rpcport=20724
  listen=1
  rpcthreads=8

  # onlynet=ipv4
  daemon=1
  gen=0

cd ~/tune/src
ps -aux | grep tune
kill -9 9913
./tuned -daemon -txindex

git clone https://github.com/iquidus/explorer.git

mongo
> use explorerdb
> db.createUser( { user: "iquidus", pwd: "3xp!0reR", roles: [ "readWrite" ] } )


cd explorer && npm install --production

cp ./settings.json.template ./settings.json
nano ./settings.json


// database settings (MongoDB)
  "dbsettings": {
    "user": "iquidus",
    "password": "3xp!0reR",
    "database": "explorerdb",
    "address": "localhost",
    "port": 27017
  },


  //update script settings
  "update_timeout": 250,
  "check_timeout": 250,

  // wallet settings
  "wallet": {
    "host": "localhost",
    "port": 20724,
    "user": "syrikx",
    "pass": "landy84"
  },




node --stack-size=10000 bin/instance


nodejs scripts/sync.js index update > /dev/null 2>&1
nodejs scripts/sync.js market > /dev/null 2>&1
nodejs scripts/peers.js > /dev/null 2>&1



crontab -e

Example crontab; update index every minute and market data every 2 minutes

*/1 * * * * cd /path/to/explorer && /usr/bin/nodejs scripts/sync.js index update > /dev/null 2>&1
*/2 * * * * cd /path/to/explorer && /usr/bin/nodejs scripts/sync.js market > /dev/null 2>&1
*/5 * * * * cd /path/to/explorer && /usr/bin/nodejs scripts/peers.js > /dev/null 2>&1




trouloeshooting:
sudo apt-get install -y mongodb-org=2.9.6 mongodb-org-server=2.9.6 mongodb-org-shell=2.9.6 mongodb-org-mongos=2.9.6 mongodb-org-tools=2.9.6


# mongo --version
MongoDB shell version: 2.6.9
# node --version
v9.4.0
