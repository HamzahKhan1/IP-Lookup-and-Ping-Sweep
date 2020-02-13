# **IP Lookup Project**

## **Objective**
- Find all domain names and corresponding IP addresses from website (www.cisco.com)
- We will do this by downloading an index page, parsing the page for domains, and writing a **for** loop to find their corresponding IP addresses.

## **Process**
- This will be performed on the command line. In my case, I am using the Terminal in Ubuntu Linux.
- Use the command `wget` to download the [Cisco](https://www.cisco.com) index page.
- Use the command `cat` to read the index.html file from cisco's website and grep “href=” in order to extract the information from the HTML file.
- Use the command `cut` and the "d" delimiter to create a command that narrows the list into domains extracted from the index.html file: `cat index.html | grep "href=" | cut -d / -f3 | grep "cisco.com" | cut -d '"' -f1 | sort –u`
- Pipe the output, which is a list of domains, into a new file called cisco.txt.
- Use the `host` command next to www.cisco.com to identify the IPV4 address, and then use the command `host www.cisco.com | grep "has address" | cut -d "" -f4` to specify what we want to see.
- To grab the corresponding IP addresses for each domain, use a **for** loop written in Nano or Vim

`-#!/bin/bash

for url in $(cat cisco.txt;)do
host $url | grep "has address" | cut -d " " -f4
done`

- Save the script and give it executable permissions: chmod 755 cisco.sh
- Execute the script with ./cisco.sh

## **Results**
- Now that the script is executed, it will generate a list of IP addresses associated with the domain names and sub domain names on cisco.com.
- Using Bash is a great way to automate the process of manually right clicking and viewing the page source or manually clicking on every link you can find.
