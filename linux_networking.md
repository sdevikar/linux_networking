# Notes

## hostnamectl

- pretty name can be set into /etc/machine

## /etc/hostname

- Can be used to set aliases, as discussed earlier
- this will allow us to do something like `ping google` instead of `ping 8.8.8.8`

## multicast dns

- some way to achieve 0 conf networking (plug n play network discovery) e.g. bonjour in apple devices

## /etc/nsswitchconf

- some configuration related to priorities of dns -- come back to this later

## dig utility

- dns lookup utility -- domain information grouper
- it performs dns lookup at the predefined dns server and returns results. e.g. you can look up what results (ip addresses) are returned for a particular website. e.g. `dig www.pluralsight.com`
- there is also an option to pass an option for a dns lookup server ip. e.g. `dig www.pluralsight.com @8.8.8.8`

# hwclock

- synchronizes the hardware clock and system time and vice versa
- system time is more of an "in-memory" time
- `date` command gives the system time
- `hwclock` gives the hardware time
- this is how the times can be synced: `hwclock hctosys` and `hwclock systohc`
