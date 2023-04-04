### DSCI6007 Sparkify Labs 3 and 4

### Task

1. Create an S3 bucket and upload the log data to it.
2. Similar to [Sparkify Lab 1](https://github.com/rara-by/Sparkify1-AWS-EC2-Flask), the query is *what are the top 10 songs and top 10 artists in descending order?* However this time, use Python instead of DBMS to compute the query. Employ parallel computing.
 
### Solution

- Create an [AWS EC2 Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html). For this project, I chose an Ubuntu 22.04 AMI and t2.micro instance. Configure a security group by adding a custom TCP rule to run Jupyter Notebook (port 8888) from anywhere (0.0.0.0 IPv4).
- SSH into the EC2 instance. Update packages and install requirements.
```
sudo apt-get update
sudo su
pip install -r requirements.txt
```
- Configure AWS CLI
```
aws configure
```
- Create and activate a virtual environment.
```
python3 -m venv venv
source venv/bin/activate
```
- Create a virtual cluster from within Jupyter Notebook.
```
ipcluster nbextension enable
```
- Start Jupyter Notebook. Copy the token generated in the output to access it from your browser following the `http://<public-dns-name>:8888/tree?token=<token here>` format.
```
jupyter notebook --port=8888 --no-browser --ip=0.0.0.0 --allow-root
```
- [Transfer](https://docs.aws.amazon.com/managedservices/latest/appguide/qs-file-transfer.html) the data directory and notebooks into the EC2 instance.
- Run `sparkify3_uploadToS3.ipynb` to create an S3 bucket and upload the log files into it. The log files aren't properly formatted as json objects. It is dealt with in the `sparkify4_displayTop10.ipynb` notebook.
- Before running the `sparkify4_displayTop10.ipynb` notebook insert 3 in the `# of engines` field under the *Ipython Clusters* tab in the Jupyter home screen.
