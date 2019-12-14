# ubuntu-sshd

Dockerized SSH service, built on top of [official Ubuntu](https://registry.hub.docker.com/_/ubuntu/) images.

## Image tags

- jtulak/ubuntu-sshd:18.04 (bionic)

## Installed packages

Base:

- Bionic (18.04) full (unminimized)

Image specific:

- OpenSSH server
- mc
- rsync
- tmux
- nmap

Config:

- `PermitRootLogin no`
- `PasswordAuthentication no`
- `ChallengeResponseAuthentication no`
- `UsePAM no`
- exposed port 22
- default user `jtulak` (uid 1000) with password `jtulak`
- mount volume to `/home/jtulak`
- default command: `/usr/sbin/sshd -D`

## Run example

```bash
$ ls -a
.ssh
$ sudo docker run -d -P -v $(pwd):/home/jtulak --name test_sshd jtulak/ubuntu-sshd:18.04
$ sudo docker port test_sshd 22
  0.0.0.0:49154

$ ssh jtulak@localhost -p 49154
jtulak@test_sshd $
```

## Security

SSH is in a reasonable configuration and allows only key-based login for a non-root user.
However, the account inside has an easy-to guess password and should be changed if deploying publicly.
If you need to use root inside of the container, you can use `sudo`.

## Issues

If you run into any problems with this image, please check (and potentially file new) issues on the [jtulak/ubuntu-sshd](https://github.com/jtulak/ubuntu-sshd/issues) repo, which is the source for this image.
