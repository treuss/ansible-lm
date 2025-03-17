# README


Dieses kleine Test-Repository enthält die Beispiele aus der Kolumne 
Admin-as-a-Service des [Linux Magazins](https://www.linux-magazin.de/), Ausgaben 
[04/2025](https://www.linux-magazin.de/magazine/2025/04/) und 
[05/2025](https://www.linux-magazin.de/magazine/2025/05/).

Beide Inventories enthalten hier natürlich nur Dummy-Daten. Hier 
bitte selbst die entsprechenden Anpassungen durchführen.


## Debian patchen

Im ersten Teil ging es darum, eine Reihe von Debian Servern effizient per 
Ansible zu patchen.


Im Inventory `servers.yml` sind die entsprechenden Debian-Server hinterlegt, 
die über das Playbook `debian_patch.yml` dann selektiert und aktualisiert 
werden. Der Parameter `--ask-become-pass` fragt dabei das Passwort ab, das
sudo für die Rechteausweitung benötigt. Der einzige Ansible-Task liegt 
hierbei im Playbook selbst.


```bash
ansible-playbook --ask-become-pass \
        --inventory inventory/servers.yml \
        debian_patch.yml
```


## Gitea Update


Beim Update von Gitea auf eine neue Version wird ebenfalls das Inventory
`servers.yml` benötigt. Nachdem ich gerne übersichtliche Playbooks habe
sind sämtliche Tasks in eine Rolle namens `gitea` ausgelagert. Im Ordner
`roles/gitea/tasks` liegt die Datei `main.yml`, die sämtliche erforderlichen
Aufgaben enthält.

All diese Aufgaben werden über die Rolle durch das Playbook angestoßen.

```bash
ansible-playbook --ask-become-pass \
        --inventory inventory/servers.yml \
        gitea_update.yml
```

