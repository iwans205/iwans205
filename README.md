install jenkins di satu server atau misal server a
setelahh itu login di web gui jenkins
install plugin, gitlab, gitlab webhhook, gitlab authentification

setelah itu di server b buat rsa
ssh-keygen -t rsa -b 4096
maka dapat id_rsa (private) dan id_rsa.pub(public)

masuk ke web gui allyoucaneat atau gitlab
masuk ke setting
masuk ke repository
masukan id_rsa.pub (public)

setelah itu ke jenkins->manage -> credential -> masukan id_rsa private
setelah itu install java di server node atau server b
registrasi ssh private key commandnya : ssh-copy-id -i /home/iwan/.ssh/iwan-test.pub iwan@localhost
new node masukan ip  server b dan pilih permanent agent
jalanin launch agent java
kalau tidak ada tanda x node tidak berjalan

setelah itu buat jobs jenkins baik freestyle ataupun pipeliine
