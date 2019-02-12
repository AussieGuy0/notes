# SSH

## Connect to git over SSH Tunnel
**Set up tunnel**

`ssh -D 8123 -f -C -q -N user@hostname`

**In ~/.ssh/config**
```
Host hostname                                                                    
    User                    git
    ProxyCommand            nc -x localhost:8123 %h %p
```

`git clone git@hostname:Project/Code.git`
