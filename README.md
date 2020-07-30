# raspi-backup

Script to periodically back up my machine to my raspberry pi backup server. Is pretty minimal, just uses headless raspbian with an external 4TB that gets mounted on boot. See [here](https://exobrain.sean.fish/raspi/) for notes I took while setting that up.

Does an `rsync` without deleting files on the remote system, provide the `-n`/`-d` flags for:

```
Backs up my system to my local raspberry pi over the network
Provide the -n option to do a --dry-run
Provide the -d option to delete any files not present on this system (--delete-before rsync flag)
```

This assumes that an `ssh` key has already been setup, that `ssh pi@<IP ADDR>` should work without a password prompt.

The `.txt` files in this directory specify which files to back up.

Expects a `RASPI_MAC_ADDR` environment variable to be set, which is used with `arp -a` to get the IP address of the pi by using the mac address. You can get the mac address by running `arp -a` and comparing the IPs with the info from running `ifconfig` on the pi. Can also `export` the `RASPI_MAC_ADDR` from a file in this directory, `./mac_addr`, like:

```
#!/bin/sh
export RASPI_MAC_ADDR="b8:27:eb:3d:42:dc"
```

### Run

Run `findpi` to make sure the pi is discoverable. Modify `configure` if necessary. Modify the `.txt` files to backup what you want to backup.

`./backup`

### Requirements

  * `arp`
  * `rsync`
  * `getopts`
  * `realpath`
  * `nmap`

