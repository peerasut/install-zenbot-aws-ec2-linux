# Using Zenbot on AWS EC2 Linux

There are 4 sections in order to use Zenbot on AWS:

1. Register AWS Account (Required Credit or Debit Card)
2. Launch Your First Instance (aka your cloud server)
3. Connect the instance
4. Install Zenbot


## Register AWS Account (need Credit/Debit Card)

1. Go to [AWS Website](https://aws.amazon.com/). Click Sign up and follow the steps.

## Launch Your First Instance

Follow the steps from [this YouTube link](https://www.youtube.com/watch?v=Qp4C6GwX5V8)


## Connect the instance by using SSH Client
**Prerequisites:** 

 - **Private key** for your instance (.pem file) which can be downloaded when creating  your instance.

**Follow these steps.**
 1. Connect to your instance using its Public DNS as states in AWS
    website.
 2. On your Terminal, change directory to where you keep the private key.
 3. Paste the command from step 1.
 4. You should be in the AWS Linux terminal by now.

## Install Zenbot
**Prerequisites:** 

 - Install Nodejs
> 
    sudo yum install nodejs
 - Verify nodejs, npm installed
> 
    node -v
    npm -v

 - Install mongodb: please follow [mongodb website](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-amazon/)
But mongodb version should be 4.4 not 5.0 (if use version 5.0 the installation will not be successful. idk why)
- Verify mongodb installed
> 
    mongo --version
- Install git
> 
    sudo yum install git
    
    # verify git installed
    git --version
**Follow these steps.**
1. Clone Zenbot Repository
> 
    git clone https://github.com/deviavir/zenbot.git
2. Change directory to zenbot directory
3. Install dependencies
> 
    npm install
    
    # if fail eg. ERR gyp, try reinstalling node-gyp
	sudo npm install -g node-gyp
	
	# then rerun step 3 again
4. Start mongodb service. Follow [mongodb website for starting service](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-amazon/)
5. Try this command to test if you can run Zenbot.
> 
    ./zenbot.sh trade binance.BTC-USDT --paper --buy_pct=20 --sell_pct=20
**If you see the trading UI. You're good to go!**

## Use `screen` command to manage terminal sessions
 - To check what screen you are in. [source](https://serverfault.com/questions/257975/how-to-check-if-im-in-screen-session)
> 
	 echo $STY
 - 
## etc.

 - To view storage left for your instance [(source)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-describing-volumes.html)
> 
    df -hT /dev/xvda1

- Copy file from local to EC2 [(source)](https://dearsikandarkhan.medium.com/files-copying-between-aws-ec2-and-local-d07ed205eefa)

On your local terminal, use secure copy command `scp` 
>
    scp -i path/to/keypair.pem /your/local/file/to/copy ec2username@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com:path/to/be/pasted
- Copy file from EC2 to local
>
    scp -i path/to/keypair.pem user@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com:path/to/be-copied/file /your/local/directory/files/to/download
You can opt out -i option to enter EC2 password when prompt.
