# test ansible on pi400
(.venv) dianluhe@0587671426 pssid % ansible -i inventory/hosts all -m ping

# configure wpa_supplicant configure file and git clone
(.venv) dianluhe@0587671426 pssid % ansible-playbook -i inventory/hosts ./playbooks/configure_wpa_supplicant.yml

# network info encryption
(.venv) dianluhe@0587671426 pssid % ansible-vault encrypt inventory/group_vars/all/wpa_supplicant_profiles.yml

# run playbook with encrypted file using passwd prompt
(.venv) dianluhe@0587671426 pssid % ansible-playbook --ask-vault-pass -i inventory/hosts ./playbooks/configure_wpa_supplicant.yml

# check ip -6
ubuntu@ubuntu:~$ ip -6 addr show

# SSH connects pi400 from mac using IPv6 local address
# https://www.itdojo.com/ssh-using-link-local-ipv6-addresses/
dianluhe@m-n4g6d2wjqp ~ % ssh ubuntu@fe80::e65f:1ff:fe18:4c96%en0

# diable services
ubuntu@ubuntu:~$ sudo systemctl --now disable \
  wpa_supplicant \
  unattended-upgrades \
  dhcpcd \
  systemd-networkd.{service,socket} \
  networkd-dispatcher
##
#   ssh connection can be recovered by IPv6 local address 
    ssh ubuntu@fe80::e65f:1ff:fe18:4c96%en0

# run pssid-80211 
ubuntu@ubuntu:/usr/local/pssid/bin$ sudo ./pssid-80211 -i wlan -c ../etc/wpa_supplicant_NETGEAR41.conf | tee 80211-start.json | jq .

# resolve date issue on pi400
sudo apt update
sudo apt install ntp
sudo systemctl enable ntp
sudo systemctl start ntp