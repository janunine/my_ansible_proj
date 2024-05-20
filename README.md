# test ansible on pi400
(.venv) dianluhe@0587671426 pssid % ansible -i inventory/hosts all -m ping

# configure wpa_supplicant configure file and git clone
(.venv) dianluhe@0587671426 pssid % ansible-playbook -i inventory/hosts ./playbooks/configure_wpa_supplicant.yml

# network info encryption
(.venv) dianluhe@0587671426 pssid % ansible-vault encrypt inventory/group_vars/all/wpa_supplicant_profiles.yml

# run playbook with encrypted file using passwd prompt
(.venv) dianluhe@0587671426 pssid % ansible-playbook --ask-vault-pass -i inventory/hosts ./playbooks/configure_wpa_supplicant.yml

