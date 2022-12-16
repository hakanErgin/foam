# anet image mods

## modifications
- removed blender process
- added to git
  - installed openssl
  - changed remote to [here](https://bitbucket.org/treedyshakan/anet/src/master/)
- installed flask:
  - added to .bashrc 
    >PATH="$PATH:/home/treedys/.local/bin"
  - added to .bashrc (to make flask work)
    >export LC_ALL=C.UTF-8
    >export LANG=C.UTF-8

  
## how to

- do something that requires sudo: (because the user name is treedys, and we don't know the password)
  >docker exec -u 0 -it *container_id* bash
- update the image with the changes in the container: 
    >docker commit *container_id* treedys/anet:test1.1_treedysuser_experimental
- version control: (we forward the host ssh key)
    >docker run -v */home/hakan/.ssh/id_rsa*:/home/treedys/.ssh/id_rsa -ti treedys/anet:test1.1_treedysuser_experimental
    or better as user
    >docker run -u treedys -v */home/hakan/.ssh/id_rsa*:/home/treedys/.ssh/id_rsa -ti treedys/anet:test1.1_treedysuser_experimental
  - in case attach from vscode doesn't work due to ownership of the `.ssh` dir: (the first command caused this)
    1. create container with volume as the root
        > docker run -u 0 -v */home/hakan/.ssh/id_rsa*:/home/treedys/.ssh/id_rsa -ti treedys/anet:test1.1_treedysuser_experimental
    2. change ownership of the folder
        > chown treedys:treedys /home/treedys/.ssh
    3. commit again