# installcentos

yum install -y epel-release

yum install -y git wget python-pip python-cryptography pyOpenSSL.x86_64 docker python-devel gcc screen

pip install ansible==2.6.3.0

git clone https://github.com/openshift/openshift-ansible

git clone https://github.com/levkov/installcentos.git

ssh-keygen -t rsa
ssh-copy-id root@console.levkov.io
ansible-playbook -i installcentos/inventory.erb ./openshift-ansible/playbooks/byo/config.yml
htpasswd -b /etc/origin/master/htpasswd admin PASSWORD123
oc login -u system:admin -n default

oadm policy add-scc-to-group anyuid system:authenticated

oadm policy add-scc-to-user privileged admin

oadm policy add-scc-to-user anyuid system:serviceaccount:myproject:mysvcacct
