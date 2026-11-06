Printers-Shares.md

Check port:

nc -vz chatelaine.cylabacademy.net 31729

List SMB shares:

smbclient -p 31729 -L //chatelaine.cylabacademy.net/

Connect to the share:

smbclient -p 31729 //chatelaine.cylabacademy.net/shares
