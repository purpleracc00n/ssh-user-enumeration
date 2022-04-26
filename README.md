# Updated - 2022

As old instances of OpenSSH on internal assessments are still a thing, I decided to made this script more useful as it can be an easy win in trying to enumerate local (and potentially domain) usernames.

The modifications consist of taking multiple hosts as targets and displaying only the valid user accounts to the console (ie. what's relevant). Also added some colour and useful debug info.

Just run it against a list of hosts with the SSH port open, it will detect the vulnerable ones and try to enumerate accounts if usernames were provided.

Example:
$ python3 sshUsernameEnumExploit.py --hostnameList ssh_targets.txt --userList users.txt --outputToDirectory

# CVE-2018-15473-Exploit
This is patched exploit of https://github.com/Rhynorater/CVE-2018-15473-Exploit for usining with new python-paramiko

On August 15th, 2018, the following advisory was posted on the OSS-Security list: [http://openwall.com/lists/oss-security/2018/08/15/5](http://openwall.com/lists/oss-security/2018/08/15/5)

The [ShelIntel team](https://www.shellntel.com/) decided to invest some time and write an exploit for this vulnerability. The exploit below has the following features:
* Threading - default 5
  * If more than 10 are used, often the OpenSSH service gets overwhelmed and causes retries
* Single username evaluation via `username` parameter
* Multiple username evaluation via `userList` parameter
* Multiple username evaluation file output via `outputFile` parameter
* Multiple output formats (list, json, csv) via `outputFormat` parameter

An example username input file is given in `exampleInput.txt`  
An example results output file in List format is given in `exampleOutput.txt`  
An example results output file in JSON format is given in `exampleOutput.json`  
An example results output file in CSV format is given in `exampleOutput.csv`  

#### Install the dependencies by running `pip install -r requirements.txt`
=======
## Build the image:
docker build -t cve-2018-15473 .

## Run the exploit:
docker run cve-2018-15473 -h

## Delete containers and image:
docker ps -a | awk '$2 == "cve-2018-15473" {print $1}' | xargs docker rm
docker rmi cve-2018-15473
