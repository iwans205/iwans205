install jenkins di satu server atau misal server a
setelahh itu login di web gui jenkins
install plugin, gitlab, gitlab webhhook, gitlab authentification

setelah itu di server jenkins /var/lib/jenkins/.ssh buat rsa
ssh-keygen -t rsa -b 4096
maka dapat id_rsa (private) dan id_rsa.pub(public)

setelah itu ke jenkins->manage -> credential -> masukan id_rsa private
setelah itu install java di server node atau server b
registrasi ssh private key commandnya : ssh-copy-id -i /home/iwan/.ssh/iwan-test.pub (user slave)@(ip node slave bukan ip server jenkins)
new node masukan ip  server b dan pilih permanent agent
jalanin launch agent java
kalau tidak ada tanda x node tidak berjalan

masuk ke web gui allyoucaneat atau gitlab
masuk ke setting
masuk ke repository
masukan id_rsa.pub (public)

setelah itu buat jobs jenkins baik freestyle ataupun pipeline
isi configure, di build trigger ceklis gitlab webhook dan url nya masukan di gitlab integration allyoucaneat dan juga generate tokennya habis itu ceklis push event
testing build now trigger

di server b di cd /var/jenkins/workspace/(nama job)
vim .git/config

tambahkan ini :
sshCommand = ssh -i /home/iwan/.ssh/iwan-test -p 45817

sehingga menjadi ini :
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
        sshCommand = ssh -i /home/iwan/.ssh/iwan-test -p 45817
[remote "origin"]
        url = ssh://git@allyoucaneat.visionplus.id:45817/website/html5.git
        fetch = +refs/heads/*:refs/remotes/origin/*

di server b  install npm, node js, quasar/cli, pm2 (untuk web)

sudo apt install npm
sudo apt install nodejs
sudo npm cache clean -f
sudo npm install -g n
sudo n stable

