SHELL=bash

.DEFAULT_GOAL := env
env: venv dep


#########################################
##### DEVELOPMENT ENVIRONMENT SETUP #####
#########################################
osdep:
	sudo apt-get install python-pip virtualenv unzip

venv: 
	rm -rf .env
	virtualenv .env

dep: pip
	PIP_CONFIG_FILE=./env/pip.conf .env/bin/pip install -r requirements.txt --upgrade

pip:
	echo "[global]" > .env/pip.conf
	echo "no-cache-dir = false" >> .env/pip.conf
	echo "index-url =  https://pypi.python.org/simple" >> .env/pip.conf

