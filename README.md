# code_challenge_iaac
per svolgere il provisioning delle due VM CentOS ho utilizzato il cloud provider AWS e ho lanciato due istanze EC2 c4.8xlarge, assegnando ad ognuna di esse un elastic ip adress. Per connettermi alle due istanze ho usato PuTTY.

ssh -i "ad.pem" centos@ec2-54-145-245-118.compute-1.amazonaws.com

lo stesso processo è stato fatto per la seconda VM.
Una volta connessomi ho creato per ogni virtual machine un user per facilitare l'interazione con ansible

useradd test

passwd test

Bisogna essere sicuri che password authentication sono permessi per il root user prima di passare al test user

cd /etc/

cd ssh

vi sshd_config

una volta fatto ciò si può passare al test user dopo un logout per ogni VM

ssh test@54.145.245.118

una volta connessi con l'ec2-user si va a aggiungere nel file etc/sudoers il test user

vi etc/sudoers

si passa al test user

su - test

una volta entrati si usa il private ip dell'altra vm

$ ssh test@3.88.77.89

si genera una chiave per far si entri nelle vm con le stesse chiavi

$ ssh key-gen

per installare ansible

$ sudo yum makecache

$ sudo yum install epel-release

$ sudo yum makecache

$ sudo yum install ansible

per gestire i server, in questo file si inseriscono i dati delle due macchine virtuali(private IPs e nome server)

$ sudo vi /etc/hosts

$ ssh-copy-id test@vm2.linuxhint.local

Si lancia questo commando su ogni server per permettere l'accesso da root senza password per l'utente

$ echo "$(whoami) ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/$(whoami)

#Una volta fatto questo si creano i file inventory.yml, requirements.yml e playbook
una volta modificato il file requiremnents si istallano roles multipli da un file

$ ansible-galaxy install -r requirements.yml

nel file inventory si vanno a definire i vari hosts dell'infrastruttura
si va a cambiare il contenuto del playbook e si lancia ansible

ansible-playbook -i inventory.yml playbook.yml -u ec2-user
