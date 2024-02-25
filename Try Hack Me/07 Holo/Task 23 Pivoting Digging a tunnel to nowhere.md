
Will download chisel 
https://github.com/jpillora/chisel/releases

but will go with sshuttle so for that will generate a ssh key and will get the access first
```
linux-admin
```
```
linuxrulez
```

```
ssh-keygen
```
![[Pasted image 20240225161434.png]]

```
cat /root/.ssh/id_rsa.pub   
```

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCw6VJ0btlpQP9zlwr/dpNMgCEQmeLNbcWIgs25zTvk1mTH/nAIxv3pNkK8ql5vR0vxY/aALwAcFd/a+DwDvbWt8qcb85dI3LcAbQkf454WDtP/Gvoqxy8Wpdr1d/uIfbEukuGe2b4jcHp/bBxwVoxqF4ZBgNNLlfK8XbSj6rnirJp2EBn8QoYHC9DwjyRRliTl/cVdy/K+UdQeGtE2oJEzptLVbiAFleR/D32c69Z1Z5aSn2gaxB5zGEs5Lm1RbZR+ATM9ibF5hMUhKiSL/wBReMIJOJZP5mfoGe3LLCoyScQi+msR48nbbXiaQKmXWwcxB9gdq/BFSuhYvzrkLZnlUpMY+VBQxeBH0v+zNw6RO2PXVVfJKO+hhuAyed9oYyw5x+lGsC2cBYcSKP7YHZB7k5C/egwoXkp6CqF9a8FNYSFrwTtonwDqo/8jeDN6V9ufEJhheK3rziG4CZREIX/mxF42A0YWkUMJpzHTXBthN5x/IP+cUIJwdQ2WCda2/h8= root@kali
```

![[Pasted image 20240225161611.png]]

```
echo 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCw6VJ0btlpQP9zlwr/dpNMgCEQmeLNbcWIgs25zTvk1mTH/nAIxv3pNkK8ql5vR0vxY/aALwAcFd/a+DwDvbWt8qcb85dI3LcAbQkf454WDtP/Gvoqxy8Wpdr1d/uIfbEukuGe2b4jcHp/bBxwVoxqF4ZBgNNLlfK8XbSj6rnirJp2EBn8QoYHC9DwjyRRliTl/cVdy/K+UdQeGtE2oJEzptLVbiAFleR/D32c69Z1Z5aSn2gaxB5zGEs5Lm1RbZR+ATM9ibF5hMUhKiSL/wBReMIJOJZP5mfoGe3LLCoyScQi+msR48nbbXiaQKmXWwcxB9gdq/BFSuhYvzrkLZnlUpMY+VBQxeBH0v+zNw6RO2PXVVfJKO+hhuAyed9oYyw5x+lGsC2cBYcSKP7YHZB7k5C/egwoXkp6CqF9a8FNYSFrwTtonwDqo/8jeDN6V9ufEJhheK3rziG4CZREIX/mxF42A0YWkUMJpzHTXBthN5x/IP+cUIJwdQ2WCda2/h8= root@kali' > author