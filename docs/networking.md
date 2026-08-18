# First network connection after installing Ubuntu

After installing Ubuntu, I connected the PC to the network using an Ethernet cable.

The Ethernet port had active LEDs, but Ubuntu did not have internet access.

## Check the network interface

I first checked the network interfaces with:

```bash
ip a
```

The Ethernet interface had an address from:

```text
169.254.x.x
```

An address in the `169.254.0.0/16` range is a link-local address. In this case it meant that the computer did not receive a normal address from DHCP.

A normal home network address would usually look something like:

```text
192.168.x.x
```

The exact address depends on the router and network configuration.

## Check NetworkManager

I checked whether Ubuntu detected the Ethernet device:

```bash
nmcli device status
```

The Ethernet device was detected and shown as connected.

That showed that Linux could see the network interface, but it did not prove that every part of the network configuration was correct. I still had to check the physical connection and DHCP.

## Find the cause

I checked the physical connection and found that the Ethernet cable was connected to the wrong or non-working network port.

I moved the cable to another Ethernet port.

After that:

- the network connection worked,
- the computer received a normal IP address,
- internet access worked.

## What I learned

The problem was not caused by a missing driver. It was a physical connection problem.

When Ethernet does not work, I should check it in this order:

1. Check the cable.
2. Check the router or switch port.
3. Check if Linux detects the network adapter.
4. Check the IP address.
5. Check DHCP.
6. Test internet access.

Useful commands are:

```bash
ip a
```

and:

```bash
nmcli device status
```

I learned that a network problem is not always caused by Linux. Sometimes the first thing to check is simply where the cable is connected.
