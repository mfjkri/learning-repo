# Set VM Network Adapter

1. Set Network Adapter to `Bridged Adapter`.

2. Boot into the VM

3. Check if VM interface is configured to `DHCP`:

   ```bash
   $ nmcli con show

   NAME                UUID                                  TYPE      DEVICE
   Wired connection 1  be505fd1-402d-45c4-8069-082d647c7e09  ethernet  eth0
   ```

   Take note of the connection NAME.

   Replace "Wired connection 1" with the NAME of the connection above.

   ```bash
   $ nmcli con show "Wired connection 1"  | grep "ipv4.method"

   ipv4.method:                            auto
   ```

   - If ipv4 is set to `auto`:

     This means that the `eth0` interface is configured using `DHCP`.

   - If set to `static`, run the following commands:

     Replace "Wired connection 1" with the NAME of the connection above.

     ```bash
     $ nmcli con mod "Wired connection 1" ipv4.method auto
     ```

4. Restart VM network interface.

   ```bash
   $ nmcli networking off
   $ nmcli networking on
   ```

5. See your new IP address.

   ```bash
   $ ip addr

   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host
        valid_lft forever preferred_lft forever
   2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
        link/ether 08:00:27:47:6d:f9 brd ff:ff:ff:ff:ff:ff
        inet 192.168.0.132/24 brd 192.168.0.255 scope global dynamic noprefixroute eth0
        valid_lft 6602sec preferred_lft 6602sec
        inet6 fe80::a00:27ff:fe47:6df9/64 scope link noprefixroute
        valid_lft forever preferred_lft forever

   ```

# Start ssh service

1. Check whether ssh service is running:

```bash
$ systemctl status ssh
```

2. If ssh is not running:

```bash
$ sudo systemctl enable ssh --now
```

# SSH into VM:

From your host machine:

```bash
$ ssh $VM_USER_NAME:$VM_IP_ADDR

#You may be prompted for a password here.
```
