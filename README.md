This source code is a simple example the way how to upload image and save it to HDFS. This program will connect HDFS via webhdfs.
Actually, it is easier than you think. The most dificulty is preparing environment to test your source code

### PREREQUISITE:
- python3
- virtualenv
- pip
- Flask==0.10.1
- Hadoop with webhdfs

### INSTALLATION:
To install Hadoop, pleas take a look at https://github.com/thanhson1085/docker-cloudera-quickstart

I will show you the detail, just hope that it will save your time.

At the first, using Docker to clone docker-cloudera-quickstart to your local.
``` 
docker pull thanhson1085/docker-cloudera-quickstart
```

And run that image, and please do not forget expose webhdfs port(50070, 50075):
```
docker run -i -t -d -p 50070:50070 -p 50075:50075 --hostname webhdfs thanhson1085/docker-cloudera-quickstart
```

There is 2 ways to run my source code. I recommend you using Docker
#### Using Docker
```
docker run -i -t -d -p 5000:5000 --hostname flask-webhdfs --link webhdfs:webhdfs thanhson1085/flask-webhdfs
```

#### Install in normal way

There is a trick here. You have to edit /etc/hosts file to your machine know where is HDFS server.
```
HDFS_IP_ADDRESS webhdfs
```

Finally, you have a HDFS Server with webhdfs support.

Clone this source code to your local
```
git clone https://github.com/thanhson1085/flask-webhdfs.git
```
Run the commands below to install and create environment to run the application
```
virtualenv -p /usr/bin/python3 env
source env/bin/activate
cp config/config.py.dev config/config.py
# And edit config.py to match your machine
pip install -r requirements.txt  
python run.py  
```
#### Test
I integrated swagger in this app. So you can use Swagger UI to test this app. And you can find swagger schema at http://localhost:5000/docs
