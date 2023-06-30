# Pritunl-Azure-VPN
Easy guide to setup a pritunl vpn on a Ubantu 22.04 Azure VM

# Setup Azure VM server 
Recommended (B1s / no need for storage/ Ubantu 22.04/ enable https & ssh ports/ Use hash instead of password)
Access through SSH port 20

# Setup Pritunl server following the steps below:

#   1. Update Apt (restart might be required)

    sudo apt update && sudo apt upgrade

#   2. Get Repo

    sudo apt install wget vim curl gnupg2 software-properties-common apt-transport-https ca-certificates lsb-release

#   3.Enter Keys (ignore deprectiation warnings)
    
    sudo tee /etc/apt/sources.list.d/pritunl.list << EOF
    deb https://repo.pritunl.com/stable/apt jammy main
    EOF
    deb https://repo.pritunl.com/stable/apt jammy main

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com --recv 7568D9BB55FF9E5287D586017AE645C0CF8E292A

#   4. Install libraries

    echo "deb http://security.ubuntu.com/ubuntu focal-security main" | sudo tee /etc/apt/sources.li                                   
    st.d/focal-security.list
    sudo apt update
    sudo apt install libssl1.1

#   5. get mongodb

    wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

# Now the VPN should be installed, time to start, and configure

#   1.  start pritunl & mongod

    sudo systemctl start pritunl mongod
    sudo systemctl enable pritunl mongod

#   2. check status (if all active and running (ctrl+c to quit monitoring))

     systemctl status pritunl mongod

#   3. go to HTTPS web portal  
HTTPS://'your server IP address'

#   4. setup-key
    sudo pritunl setup-key

#   5. Admin credentials
    sudo pritunl default-password


#  now everything should be setup and working, keep in mind while setting up new server to take the port number for the vpn and adding an inbound rule to allow access for that port in azure
