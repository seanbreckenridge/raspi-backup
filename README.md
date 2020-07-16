# raspi-backup

Scripts for periodically backing up my machine to my local raspberry pi backup server. Is pretty minimal, just uses an raspbian with an external 4TB that gets mounted on boot. See [here](https://exobrain.sean.fish/raspi/) for notes I took while setting that up.

Does an `rsync` without deleting files on the remote system, provide the `-n`/`-d` flags for:

```
./backup -h
Backs up my system to my local raspberry pi over the network
Provide the -n option to do a --dry-run
Provide the -d option to delete any files not present on this system (--delete-after rsync flag)
```

This assumes that an `ssh` key has already been setup, that `ssh pi@<IP ADDR>` should work without a password prompt.

The `.txt` files in this directory specify which files to back up.

Expects a `RASPI_MAC_ADDR` environment variable to be set, which is used with `arp -a` to get the IP address of the pi by using the mac address. You can get the mac address by running `arp -a` and comparing the IPs with the info from running `ifconfig` on the pi.

### Run

Run `findpi-ip` to make sure the pi is discoverable. Modify `config` if necessary. Modify the `.txt` files to backup what you want to backup.

`./backup`

### Requirements

  * `arp`
  * `rsync`
  * `getopts`
  * `realpath`
  * `nmap`

