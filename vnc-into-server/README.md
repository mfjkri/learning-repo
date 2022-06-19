### Note: Replace `apt` with whatever package manager you are using for your server machine.

&nbsp;

# Install Desktop Environment

#### ❗️ Note: You can skip to [Install VNC](#install-vnc) if you server already has a desktop environment.

For this guide I will be installing `XFCE`:

```bash
$ sudo apt update

$ sudo apt install xfce4 xfce4-goodies
```

&nbsp;

# Finish up installation

Just some last few packages to install.

```bash
$ sudo apt update

$ sudo apt install gnome-core kali-defaults kali-root-login desktop-base
```

You will be prompted here to select your display manager:

    gdm3 or lightdm

For the purpose of this guide, we will be choosing `lightdm`.

&nbsp;

# Install VNC

I will be installing `TightVNC` as our VNC server.

```bash
$ sudo apt update

$ sudo apt install tightvncserver
```

&nbsp;

# Configuring VNC Server

Here we will be setting the screen resolution of the vnc to be `1024px by 768px`.\
You can change the resolution to whatever you like.

```bash
$ tightvncserver -geometry 1024x768
```

You will be prompted here to set a password (`$VNC_PASSWORD`) and confirm it.

To check if the vnc server is already running:

```bash
$ netstat -tupln
```

Take note of the `port` number the vnc server is listening to.

&nbsp;

---

---

&nbsp;

# Connecting to the VNC Server from host

## Using Windows as your host machine:

1. Start the VNC tunnel using `SSH`.

   ```bash
   $ ssh -L 5901:localhost:5901 -N -f $USERNAME:$IP_ADDR -i /path/to/key
   ```

- `$USERNAME` and `$IP_ADDR` are the same ones you would use to just ssh into the machine.

- `5901:localhost5901`:

  - The first `5901` is the port number your VNC server is listening to.
  - The second `localhost:5901` is the port number to forward it to on your host machine.

- `-i /path/to/key` is to provide the key for authenticated:

  If your configuration does not use one, leave out this argument.

2. Install `Real VNC Viewer` for Windows.

3. Run `Real VNC Viewer`.

4. Enter in `localhost:5901` in the textbox.

5. You will be prompted for a password:

   This password is the one set when configuring you VNC Server for the first time.

   In our case the password is `$VNC_PASSWORD`.

&nbsp;

## Using Linux as your host machine:

The steps for a Linux host machine is very similar to a Windows one.

The only difference lies in the `VNC Viewer` you choose:

- Either a GUI one similar to Windows

- Or a CLI one

- Or one with both options available
