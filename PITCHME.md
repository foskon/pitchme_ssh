
---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Splash</span>

# SSH
## The good way

---

<span class="menu-title" style="display: none">SSH keys</span>

### <span class="gold">SSH keys</span>

+++
---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Checking for existing SSH keys</span>

### <span class="gold">Checking for existing SSH keys</span>

<br>

```
ls -al ~/.ssh
```

<br>

- This will show a list of ssh key files stored in your computer. <!-- .element: class="fragment" -->

+++

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Generate a SSH key</span>

### <span class="gold">Generate a SSH key</span>

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

<br>

- This creates a new ssh key, using the provided email as a label. <!-- .element: class="fragment" -->

+++

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Testing connection</span>

### <span class="gold">Testing connection</span>

```
ssh -T git@github.com
```

<br>

```
Hi username! You've successfully authenticated, but GitHub does not
provide shell access.
```

+++

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">You may see this warning</span>

- You may see this warning:

<br>

```
The authenticity of host 'github.com (192.30.252.1)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?
```

---

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">SSH Config File Structure</span>

### <span class="gold">SSH Config File Structure</span>

* Each user on your local system can maintain a client-side SSH configuration file.

* It allows you to store your common connection items and process them automatically on connection. <!-- .element: class="fragment" -->

---

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Location of the SSH Client Config File</span>

### <span class="gold">Location of the SSH Client Config File</span>

<br>

```
~/.ssh/config
```

<br>

Often, this file is not created by default, so you may need to create it yourself <!-- .element: class="fragment" -->

---

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Configuration File Structure</span>

### <span class="gold">Configuration File Structure</span>

```
Host firsthost
    SSH_OPTION_1 custom_value
    SSH_OPTION_2 custom_value
    SSH_OPTION_3 custom_value

Host secondhost
    ANOTHER_OPTION custom_value

Host *host
    ANOTHER_OPTION custom_value

Host *
    CHANGE_DEFAULT custom_value
```

<span class="code-presenting-annotation fragment current-only" data-code-focus="1-1, 6-6, 9-9, 12-12" >SSH will match the hostname given on the command line with each of the Host headers that define configuration sections.</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="1-1, 6-6, 9-9, 12-12" >It will do this from the top of the file downwards, so order is incredibly important.</span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="2-4, 7-7, 10-10, 13-13" >This are options for each Host header</span>

---

<span class="menu-title" style="display: none">SSH Configuration Options</span>

### <span class="gold">SSH Configuration Options</span>

+++

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Host</span>

#### <span class="gold">Host</span>

- An alias you whant to use. When the first matching Host definition is found, each of the associated SSH options are applied to the upcoming connection.

<br>

```
# Github foskon@gmail.com
    Host github_personal
```

+++

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">HostName</span>

#### <span class="gold">HostName</span>

- The actual hostname that should be used to establish the connection. This replaces any alias defined in the Host header.

<br>

```
# Github foskon@gmail.com
    Host github_personal
    HostName github.com
```

+++

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">User</span>

#### <span class="gold">User</span>

- The username to be used for the connection.

<br>

```
# Github foskon@gmail.com
    Host github_personal
    HostName github.com
    User git
```

+++

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Port</span>

#### <span class="gold">Port</span>

- The port that the remote SSH daemon is running on. 

```
# Github foskon@gmail.com
    Host github_personal
    HostName github.com
    User git
    Port 22
```

<br>

Only necessary if the remote SSH is not running on the default port 22. <!-- .element: class="fragment" -->

+++

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">IdentityFile</span>

#### <span class="gold">IdentityFile</span>

- This option can be used to specify the location of the key to use for each host. 

```
# Github foskon@gmail.com
    Host github_personal
    HostName github.com
    User git
    Port 22
    IdentityFile ~/.ssh/foskon-GitHub
```

<br>

If your keys are in the default locations, each will be tried and you will not need to adjust this. <!-- .element: class="fragment" -->

---

<span class="menu-title" style="display: none">Examples</span>

### <span class="gold">Examples</span>

---

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Example 2</span>

```
# Github foskon@gmail.com
    Host github_personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/foskon-GitHub
```

<br>

#### This host allows us to connect as <span class="gold">git@github.com</span> using the key file <span class="gold">~/.ssh/foskon-GitHub</span> by typing this on the command line:

```
ssh github_personal
```

---

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Example 3</span>

```
# Github carlos.manzanas@intelygenz.com
    Host github_work
    HostName github.com
    User git
    IdentityFile ~/.ssh/IGZCarlosManzanas-GitHub
```

<br>

#### This host allows us to connect as <span class="gold">git@github.com</span> using the key file <span class="gold">~/.ssh/IGZCarlosManzanas-GitHub</span> by typing this on the command line:

```
ssh github_work
```

---

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">Example 1</span>

```
# Raspberry Pi 3
    Host raspberry
    HostName your.custom.domain.net
    User pi
```

<br>

#### This host allows us to connect as <span class="gold">pi@your.custom.domain.net</span> by typing this on the command line:

```
ssh raspberry
```

---

---?image=assets/bg_stars.jpg

<span class="menu-title" style="display: none">References</span>

## <span class="gold">References</span>

<br>

#### https://www.digitalocean.com/community/tutorials/how-to-configure-custom-connection-options-for-your-ssh-client <!-- .element: class="fragment" -->
#### https://help.github.com/articles/testing-your-ssh-connection/ <!-- .element: class="fragment" -->
#### https://gitpitch.com <!-- .element: class="fragment" -->

---

---?image=assets/thats_all.gif

---

---?image=assets/bg_stars.jpg

### <span class="gold">I don't believe in live demos but...</span>

---

---?image=assets/bg_stars.jpg

### <span class="gold">DEMO</span>
