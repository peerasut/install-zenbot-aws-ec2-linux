
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

 - Install Nodejs by follow [this aws tutorial link](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html)

 - Verify nodejs, npm installed
> 
    node -v
> 
    npm -v
 - Install mongodb by follow [this mongodb link](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-amazon/)
For Linux ARM64 use [this link](https://dev.to/bobstrange/install-mongodb-to-arm64-amazon-linux-2-lon) to install mongodb and just use version 4.4 don't use 5.0
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

On your local terminal, use `scp` (secure copy) command  
>
    scp -i path/to/keypair.pem /your/local/file/to/copy ec2username@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com:path/to/be/pasted
- Copy file from EC2 to local
>
    scp -i path/to/keypair.pem user@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com:path/to/be-copied/file /your/local/directory/files/to/download
You can opt out -i option to enter EC2 password when prompt.

In case that you have already configured alias for that EC2 in ssh config. You can use that alias, for example,
>
    scp alias:path/to/be-copied/file /your/local/directory/files/to/download


- Secure your key pair with `chmod` command [(source)](https://www.howtogeek.com/437958/how-to-use-the-chmod-command-on-linux/)
>
    chmod nmo /path/to/keypair.pem
 Where n, m, o is number for allow permission. Note that n is for you who own the file, m is for group permission and o is for other than the first two.
-   0: (000) No permission.
-   1: (001) Execute permission.
-   2: (010) Write permission.
-   3: (011) Write and execute permissions.
-   4: (100) Read permission.
-   5: (101) Read and execute permissions.
-   6: (110) Read and write permissions.
-   7: (111) Read, write, and execute permissions.

For example, to make only you can read the file use
>
    chmod 400 /path/to/keypair.pem
To check permission for a file (more info go to the  [source](https://www.howtogeek.com/437958/how-to-use-the-chmod-command-on-linux/))
>
    ls -l keypair.pem
