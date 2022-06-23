# Github Action SSH Error

`ssh: handshake failed: ssh: unable to authenticate, attempted methods [none publickey], no supported methods remain`

`sudo vi /etc/ssh/sshd_config`

_아래의 두 항목 설정 및 저장_

    PubkeyAuthentication yes
    PubkeyAcceptedKeyTypes=+ssh-rsa
