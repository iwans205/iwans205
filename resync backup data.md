cara resync backup data
bikin ssh terlebih dahulu
ssh-keygen -t rsa -b 4096

setelah itu ssh key di copy ke ip server tujuan
ssh-copy-id -i /home/iwan/.ssh/iwan-test.pub mncnow@10.10.19.240

setelah itu coba ssh ke server tujuan
ssh -i .ssh/iwan-test mncnow@10.10.19.240

setelah itu buat resync ke server yang mmau di tuju
rsync -Pav -e "ssh -i /home/iwan/.ssh/iwan-test" /home/mncnow/iwan.py mncnow@10.10.19.240:/home/mncnow

rsync -Pav -e "ssh -i -> command tetap 
/home/iwan/.ssh/iwan-test" -> ini adalah ssh keynya
/home/mncnow/iwan.py -> ini adalah file yang mau di backup
mncnow@10.10.19.240:/home/mncnow -> server tujuan
