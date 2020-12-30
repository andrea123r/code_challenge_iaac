# code_challenge_iaac
per svolgere il provisioning delle due VM CentOS 7 ho utilizzato il cloud provider AWS e ho lanciato due istanze EC2 c4.8xlarge, assegnando ad ognuna di esse un elastic ip adress.
Per far questo ho installato Vagrant sulla mia macchina host e inoltre il plugin vagrant-aws da VS code, per macchina windows:

vagrant plugin install C:\Users\andre\Downloads\vagrant-aws-0.8.0.gem

Una volta installata anche l'estensione di vim su VS code ho modificato il vagrant file. Ho modificato il file dopo aver lanciato questo commando: 

vagrant box add aws https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box

in questa repo c'è un esempio di Vagrantfile. Nel mio vagrant file ho inserito la configurazione delle due istanze EC2 di AWS e il provisioning con Ansible.
