## Connect to Ubuntu server with Git Bash
chmod 400 "shopbondhu-web-public.pem"
ssh -i "shopbondhu-web-public.pem" ubuntu@13.210.117.22

## Ubuntu Command
sudo apt update
sudo apt upgrade
sudo apt install nginx -y
sudo systemctl status nginx
sudo apt install nodejs npm -y
clear
git clone https://github.com/sumaya-shemo/shopbondhu.git
ls -la
cd shopbondhu
npm i
npm run dev
history