## Mājasdarbs - 5. Tēma

### Izveidotās instances:
![instances](images/instances.jpg)

## 6. Nomainīt **hostname** katram serverim
1. sudo vim /etc/hostname
2. Jāsamaina hostname 
3. sudo reboot

Rezultāts:
```sh
ubuntu@master-dainis-banders:~$ hostname
master-dainis-banders
```
```sh
ubuntu@host-1-dainis-banders:~$ hostname
host-1-dainis-banders
```
```sh
ubuntu@host-2-dainis-banders:~$ hostname
host-2-dainis-banders
```

## 7.Uzstādiet **Ansible** programatūru uz master-dainis-banders
```sh
echo "sysops ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/sysops
sudo apt update
sudo apt upgrade -y
sudo reboot
sudo apt install -y software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt update
sudo apt install -y ansible
ansible --version
```

## 8. Rediģēt **Ansible inventory** host pievienojot host instances
Jāpievienot failā `/etc/ansible/hosts` host instances:
```
[servers]
host-1-dainis-banders
host-2-dainis-banders

[webservers]
host-1-dainis-banders

[database]
host-2-dainis-banders
```
## 9. Konfigurēt ssh atslēgu starp Master un host serveriem
```ssh
ssh-keygen -b 2048 -t rsa
```
Jāiekopē publiskā atslega iekš **host-1-dainis-banders** un **host-2-dainis-banders** `~/.ssh/authorized_keys`

## 10. Pārbaudiet Ansible serveru konfigurāciju ar Ansible komandu **ansible-inventory --list -y**
```
all:
  children:
    database:
      hosts:
        host-2-dainis-banders: {}
    servers:
      hosts:
        host-1-dainis-banders: {}
        host-2-dainis-banders: {}
    ungrouped: {}
    webservers:
      hosts:
        host-1-dainis-banders: {}
```
## 11. Veiciet visu Ansible host ping ar Ansible ping komandu.
```ssh
host-1-dainis-banders | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
host-2-dainis-banders | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
## 14. Izpildiet Ansible Ad hoc komandu lai nolasītu host serveros esošos procesus.
```ssh
ansible host-1-dainis-banders -m shell -a 'ps -ef'
ansible host-2-dainis-banders -m shell -a 'ps -ef'
```

## 15. Noklonējiet repozitoriju uz Master nodes https://github.com/lu-vumc-devops/lu-vumc-devops.ansible.git
```ssh
git clone https://github.com/lu-vumc-devops/lu-vumc-devops.ansible.gi
```

## 16. Pārveidojiet failu **AdditionalPackages.yml** ta lai http tiktu uzstādīts uz host1 un datubāzes uz host2. Veiciet testu.
ansible-playbook [AdditionalPackages.yml](AdditionalPackages.yml)

## 17. Attiecīgi pārveidojiet **AdditionalPackagesDelete.yml** lai delete notiktu tajos serveros kur iepriekš tika uzstādīts http un mariadb.

ansible-playbook [AdditionalPackagesDelete.yml](AdditionalPackagesDelete.yml)

## 18 WebSuperPage.yml
ansible-playbook [WebSuperPage.yml](WebSuperPage.yml)

## 19. Veiciet pārbaudi vai ar publisko IP Jums veras vaļa lapa. Pārbaudiet attiecīgus AWS iestādījumus
[AWS inbound rules](images/inbound_rules.png)
[Mājas lapa](images/index.html.png)
