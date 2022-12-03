+++
title = "Ansible"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-11T05:00:00Z
description = "ansible"
categories = ["technology"]
type = "post"

+++
#### Installation

```
sudo apt update
sudo apt upgrade
sudo apt install software-properties-common
```
`list.d/ansible.list:`

Add the following line to /etc/apt/sources.list or /etc/apt/sources.

`deb http://ppa.launchpad.net/ansible/ansible/ubuntu focal main`

Then run these commands:

\
for Debian 11 (Bullseye):
```
sudo apt install gnupg2
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
sudo apt update
sudo apt install ansible
```

\
`mkdir ansible_test`

`cd ansible_test/`


**Config file:**

`touch ansible.cfg`

`nano ansible.cfg`
```
[defaults]
inventory=inventory
host_key_checking=False
```


**Inventory file**

`touch inventory`

`nano inventory`

```
[master]
192.168.1.238

[nodes]
192.168.1.239

[master:vars]
ansible_ssh_user=sedat
ansible_ssh_pass=sedatpass

[nodes:vars]
ansible_ssh_user=sedat
ansible_ssh_pass=sedatpass
```
`ansible nodes -m ping`

`ansible nodes -m shell -a "cat /etc/os-release"`

`nano install_nettools.yml`
```
---
- hosts: master
  become: yes
  tasks:
    - name: install net-tools
      apt:
        name: net-tools
```

`ansible-playbook install_nettools.yml -K`

*-K mean running as sudo*

238 makinasina nettols yuklenecektir.yani bulundugumuz master makinasinda net-tools yuklendi.

simdi masterdan bunu kaldirip ayni anda 239 makinasina net-toolsu yukleyelim.bunun icin kullanacagimiz yml dosyasi:

ama once inventorye -K ile sudo sifresi girmemek icin her client icin sudo passowrklerini yazalim.

sedat@debian:~/ansible_test$ `nano inventory`

```
[master]
192.168.1.238

[nodes]
192.168.1.239


[master:vars]
ansible_ssh_user=sedat
ansible_ssh_pass=sedatpass
ansible_become_pass=sedatpass

[nodes:vars]
ansible_ssh_user=sedat
ansible_ssh_pass=sedatpass
ansible_become_pass=sedatpass
```
sedat@debian:~/ansible_test$ `nano install_nettools.yml`
```
---
- hosts: master
  become: yes
  tasks:
    - name: remove net-tools
      apt:
        name: net-tools
        state: absent
- hosts: nodes
  become: yes
  tasks:
    - name: install net-tools
      apt:
        name: net-tools
        state: present
```
sedat@debian:~/ansible_test$ `ansible-playbook install_nettools.yml`

absent olandan net-tools kaldirilacaktir.present olanda yuklenecektir.komutu yazdigimzda sifre sormadan islemi yapacaktir.

simdi makinalara public keyleri yukleyelim.once kendimiz public key olusturalim.

`cd ~./.ssh`

`ssh-keygen`

isim sordugunda ansible_id_rsa yazalim ok ok diyip onaylayalim.

simdide yeni yml dosyasi olusturalim.

`nano add_public_keys.yml`

```
---
- hosts: master
  become: yes
  tasks:
    - name: install public keys
      ansible.posix.authorized_key:
        user: sedat
        state: present
        key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
- hosts: nodes
  become: yes
  tasks:
    - name: install public keys
      ansible.posix.authorized_key:
        user: sedat
        state: present
        key: "{{ lookup('file', '~/.ssh/ansible_id_rsa.pub') }}"
```
simdide bu komutu calistirarak clientlara bu keyi upload edelim.

`ansible-playbook add_public_keys.yml`



ornegin bu sekilde /etc/sudoers dosyasini editleyip sudoda sifre girilmeden islem yapilmasini saglayabiliriz.
```
---
- hosts: all

  become: yes
  tasks:

  # Installs public key
  # --
  #
  - name: install public keys
    ansible.posix.authorized_key:
      user: "{{ lookup('env','USER') }}"
      state: present
      key: "{{ lookup('file', '~/.ssh/id_rsa.pub') }}"

  # (Optional)
  # Set all sudoers to no password
  # --
  - name: change sudoers file
    lineinfile:
      path: /etc/sudoers
      state: present
      regexp: '^%sudo'
      line: '%sudo ALL=(ALL) NOPASSWD: ALL'
      validate: /usr/sbin/visudo -cf %s
```
bunu calistirdikdan sorna ansible.cfg deki host_key_checking=False satirini kaldiriyoruz.

cunku bu sadece kullanici adi ve parola authentication icindi

ayrica inventorydeki 
```
ansible_ssh_pass=sedatpass
ansible_become_pass=sedatpass
```
satirlarini da kaldiriyoruz.


```
[master]
192.168.1.238

[nodes]
192.168.1.239


[master:vars]
ansible_ssh_user=sedat
ansible_ssh_private_key_file=~/.ssh/ansible_id_rsa

[nodes:vars]
ansible_ssh_user=sedat
ansible_ssh_private_key_file=~/.ssh/ansible_id_rsa
```

`ansible all -m ping`

dedigimizde artik sifre olmadan makinalari pingleyebildigimizi gorecegiz.

ayrica bu komutunda calistigini gorecegiz.bisey degismeyecek daha once calistirdik ancak auth oldugunu gorecegiz

`ansible-playbook add_public_keys.yml`