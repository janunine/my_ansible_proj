(.venv) dianluhe@0587671426 pssid % ansible -i inventory/hosts all -m ping

(.venv) dianluhe@0587671426 pssid % ansible-playbook -i inventory/hosts ./playbooks/configure_wpa_supplicant.yml