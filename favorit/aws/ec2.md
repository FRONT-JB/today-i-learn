# Github Action SSH Error

`ssh: handshake failed: ssh: unable to authenticate, attempted methods [none publickey], no supported methods remain`

`sudo vi /etc/ssh/sshd_config`

_아래의 두 항목 설정 및 저장_

    PubkeyAuthentication yes
    PubkeyAcceptedKeyTypes=+ssh-rsa

---

`github action not found error`
[stackoverflow](https://stackoverflow.com/questions/62863080/github-actions-err-bash-line-3-npm-command-not-found)

_yarn not found, pm2 not found, node not found 에러_

원인 : nvm으로 node를 설치했을 때 발생함

```bash
sudo ln -s ~/.nvm/versions/node/<NodeVersion>/bin/yarn /usr/local/bin/yarn
```

```bash
sudo ln -s ~/.nvm/versions/node/<NodeVersion>/bin/pm2 /usr/local/bin/pm2
```

```bash
sudo ln -s ~/.nvm/versions/node/<NodeVersion>/bin/node /usr/local/bin/node
```
