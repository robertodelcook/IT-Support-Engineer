# IT Support engineer Questions


## How to submit the answers

1. Create a GitHub Account
1. Git Clone this repository to your local machine
1. Remove the current `origin` remote (`git remote remove origin`)
1. Create a new repository under your GitHub account (do **NOT** fork this repository)
1. Follow the instructions to `push an existing repository from the command line...`
1. Create a branch called `add_answers` on your local machine
1. Add answers to this Document (using a simple Text editor), commit your answers to the `add_answers` branch
1. Push your `add_answers` branch to your personal remote `origin`
1. Send a notification to your contact at Honestbee with a link to your repository

If any of the steps above is unclear, please try GitHub user guides first, then ask your contact at Honestbee to clarify. 

The method of submission is part of the test (usage of Git) - but we won't use `forks` or `pull requests`. 

## Questions

1.  A vendor is trying to connect to a server we publicly expose (assume we are not using VPN). When asked for his public IP from which he will be connecting, the vendor provides us with the following IP `192.168.0.100`, what should be our next steps? 

    1.  Include questions we may need to ask to get additional information to ensure this vendor will be able to connect over the public internet to our server. __Note that this vendor is not in our LAN, nor on a VPN with us__.

        > Add follow up Questions here as a bulleted list and add an explanation why you ask each question (what do you expect to receive back)

        a) vendor should provide the specific host and port info to be whitelisted.
    Explanation- The reason we ask this information from vendor is to get his IP and Host details so that we can allow his IP in our network on the shared port given by vendor(80 or 443).

	b) What security protocol should be followed for exchanging data/msgs
    Explanation:-  Network security protocols are primarily designed to prevent any unauthorised user, application, service or device from accessing network data. This applies to virtually all data types regardless of the network medium used.
We need this information so that we know by which mechanism vendor will be accessing the server (SFTP, HTTPS, SSL)

	c) URL filtering rules to be applied on your side in case if its a web call

	d) If its non-web call, then ACL ( Access control list ) to be provided
    Explanation: We need information above to perform security to our server as Rules and filtering to be done on the target server,To avoid any malicious attempts to traverse other web page on the server
 



    1.2  Write a PowerShell command (assume Windows 2012 R2) to add a new firewall rule on a single server, allowing incoming connections on port `3389` for `TCP` protocol __limited to the public IP of the vendor only__ (assuming we have the public IP of the vendor)

    ```powershell
    # netsh advfirewall firewall add rule name="192.168.0.100" dir=in action=allow protocol=TCP localport=3389

    ```

2.  How do you list all Computers in an Active Directory Domain using Powershell (output DNSHostname in a table format, no need for `filters` or `SearchBase`)

    ```powershell
    # Import-Module ActiveDirectory  
    Get-ADComputer -Filter * -Properties * | FT Name,DistinguishedName -a | Export-CSV AllComputers.csv -NoTypeInformation -Encoding UTF8

    ```

3.  What could possible troubleshoot tests be for the following output on a macOS machine. 
    
    For each step, mention what would be your next step

    ```bash
    $ ping microsoft.com
    PING microsoft.com (23.100.122.175): 56 data bytes
    Request timeout for icmp_seq 0
    Request timeout for icmp_seq 1
    ...
    ```

    Notes:

    -   Local machines in the same network can still be pinged by IP
    Answers
    
       a) The First thing we will do i to verify if DNS entries are present for the  host (microsoft.com).
	
	b) If the DNS entry present is correct the next action will be to perform the ping test on atleast 2 different machines, the reason I would do this, is to get a high level overview of the issue, testing on one machine could yield a false positive.   
	
	c) If the issue still persists then we will try and flush the DNS cache by running following command-  run ifconfig /flushdns and ifconfig /release - 
	
	D) If even after clearing DNS cache issue still persist then we need to check if server computers use a restrictive firewall which is blocking the ICMP packets from unknown hosts.

Thank you for your time.
