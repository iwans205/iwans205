bikin file bernama resync
vim resync.sh

edit vim resync

#!/bin/bash
rsync -Pav -e "ssh -i /home/iwan/.ssh/iwan-test" /home/mncnow/iwan.py mncnow@10.10.19.240:/home/mncnow


note :
#!/bin/bash -> untuk menjalankan filenya

setelah itu
chmod 755 resync.sh

untuk mengubah file resync.sh agar bisa dijalankan
./resync.sh

untuk menjalankan scriptnya
