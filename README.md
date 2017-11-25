# Coding Notes #

1. [Setting up azure / nginx / webapps](#azure)



## <a name="azure"></a>1. Setting up azure / nginx / DNS / webapps ##

### Setup Azure ###

1. Add resource, ubuntu, select level, deploy
1. Install nginx: `apt-get install nginx`
1. Start up nginx: `sudo service nginx start`
1. Open up HTTP in Network Security Group in azure:
   * Click on VM resource-nsg
   * Click Inbound Security Rules
   * Click Add
   * Click Advanced, and use the "Service" dropdown to select "HTTP"
1. Try navigating to IP in web browser to see nginx welcome page
    
### Setup nginx ###

* If you want to have nginx be able to run multiple sites, you need to remove the "default server" tag from the server's "listen" line for each site config.
* Add the following line to the `http` section of /etc/nginx/nginx.conf to prevent any random subdomains from resolving to your default site:

		server {
    		return 404;
    	}
    
### Connect DNS to IP ###

* Instructions taken from: [here](https://help.duda.co/hc/en-us/articles/219543667-Register-com-Domain-Set-up)
* Register.com manage domain. Use default DNS.
* Edit CNAME record
   * Before the URL: www
   * Points to: a.\<domain\>.com
       * (I don't know why we need the 'a', it can be any letter. I haven't tried leaving it out)
* Edit IP address record:
	* Name/Alias: @
	* Target/Destination: \<ip address here\>
