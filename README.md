# Coding Notes #

1. [Basic emacs setup](#emacs)
2. [Setting up azure / nginx / webapps](#azure)
3. [Setting up nvm / node / npm](#nvm)
4. [Setting up python on ubuntu](#python_ubuntu)
5. [Setting up flask / vue / webpack / socket.io](#flask_vue_webpack)


## <a name="emacs"></a>1. Basic emacs setup
* Emacs-25 on Ubuntu:
	* sudo add-apt-repository ppa:kelleyk/emacs
	* sudo apt-get update
	* sudo apt-get install emacs25-nox
* .emacs:

		(require 'package)
		(package-initialize)
		(add-to-list 'package-archives '("melpa" . "http://melpa.milkbox.net/packages/") t)
		
		(global-set-key (kbd "C-c e") 'eshell)
		(global-set-key (kbd "C-c q") 'query-replace-regexp)
		(delete-selection-mode 1)


## <a name="azure"></a>2. Setting up azure / nginx / DNS / webapps ##

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

## <a name="nvm"></a>3. Setting up nvm / node / npm ##

1. `wget https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh`
2. `bash install.sh`
3. `nvm install node`
4. `nvm use node`

## <a name="python_ubuntu"></a>4. Setting up python on ubuntu ##

1. `sudo apt-get install python-pip`
2. `sudo apt-get install python3-pip`
3. `pip3 install -U pip`
4. `pip3 install virtualenv`

## <a name="flask_vue_webpack"></a>5. Setting up a flask / vue / webpack / socket.io project ##

1. `npm init vuetifyjs/webpack`
2. Edit **package.json**. Add `--host 0.0.0.0` to the dev section
3. Edit the **webpack.config.js** file

	- add the following lines to **devServer**:

			proxy: {
				'/socket.io': 'http://localhost:5000'
			},
			disableHostCheck: true,
	- add the following line to alias: `'@': path.resolve('src'),`
4. Install more node packages

		npm install vue-router
		npm install vue-socket.io
		npm install vuex