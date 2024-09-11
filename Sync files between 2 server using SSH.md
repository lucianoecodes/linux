# Sync files between 2 server using SSH

# Generate public key for ssh

1) Step 1 – Generate RSA keys on the source server

ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:

2) Step 2 – Copy the key to the destination server

ssh-copy-id -i root@target-server-domain-or-ip.com
root@target-server-domain-or-ip.com's password:
Now try logging into the machine, with "ssh 'root@target-server-domain-or-ip.com'", and check in:
.ssh/authorized_keys
to make sure we haven't added extra keys that you weren't expecting.



# Create script to sync your files

for sync2 in $(cat /usr/local/projects/projects_names.txt); do

  PROJECT2=$(echo "$ync2" | cut -d, -f3)

  echo "$PROJECT2"

  cd /usr/local/projects/$PROJECT2

  rsync -Pcuv -e ssh `find . -name "*.csv" -type f -mtime -4` root@10.10.10.22:/home/user1/$PROJECT2

  sleep 2

done
