# HDLC (Default Cisco) Configuration

## What is HDLC?

**HDLC (High-Level Data Link Control)** is a **Layer 2 WAN protocol** used for communication over serial links between routers.

On Cisco routers, **Cisco HDLC is the default encapsulation protocol** on serial interfaces. This means that when you configure and activate a serial interface, it normally uses HDLC automatically unless you change the encapsulation to another protocol such as PPP.

HDLC is used to encapsulate data and send it across a **point-to-point serial connection**.

In this lab, two Cisco 2911 routers, **R1 and R2**, are connected using a serial link. The network between them is **10.10.10.0/30**.

---

# Network Topology

```text
+-----------------------+                         +-----------------------+
|          R1           |                         |          R2           |
|      Cisco 2911       |                         |      Cisco 2911       |
|                       |       Serial Link       |                       |
|  Interface: Se0/3/0   |=========================|  Interface: Se0/3/0   |
|  IP: 10.10.10.1/30    |     10.10.10.0/30       |  IP: 10.10.10.2/30    |
+-----------------------+                         +-----------------------+
```

## IP Addressing Table

| Device | Interface    | IP Address | Subnet Mask     |
| ------ | ------------ | ---------- | --------------- |
| R1     | Serial 0/3/0 | 10.10.10.1 | 255.255.255.252 |
| R2     | Serial 0/3/0 | 10.10.10.2 | 255.255.255.252 |

---

# Step 1: Create the Topology

1. Open **Cisco Packet Tracer**.
2. Add two **Cisco 2911 routers**.
3. Make sure the routers have serial interfaces available. If necessary, power off the router and add a serial module.
4. Connect the routers using a **Serial DCE cable**.

Connect:

```text
R1 Serial 0/3/0  <-------->  R2 Serial 0/3/0
```

One side of the serial connection will be the **DCE side**. The DCE side provides clocking and requires the `clock rate` command.

---

# Step 2: Configure R1

Enter the following commands on R1:

```bash
enable
configure terminal

interface serial 0/3/0
ip address 10.10.10.1 255.255.255.252
no shutdown

end
```

Because **Cisco HDLC is the default encapsulation**, you do not need to configure it manually.

However, you can verify or explicitly configure it using:

```bash
configure terminal
interface serial 0/3/0
encapsulation hdlc
no shutdown
end
```

If R1 is the **DCE side**, configure a clock rate:

```bash
configure terminal
interface serial 0/3/0
clock rate 64000
end
```

---

# Step 3: Configure R2

Enter the following commands on R2:

```bash
enable
configure terminal

interface serial 0/3/0
ip address 10.10.10.2 255.255.255.252
no shutdown

end
```

You can also explicitly configure HDLC:

```bash
configure terminal
interface serial 0/3/0
encapsulation hdlc
no shutdown
end
```

> **Note:** Only the router connected to the **DCE side** needs the `clock rate` command.

---

# Step 4: Verify the Serial Interfaces

On both routers, use:

```bash
show ip interface brief
```

The serial interface should show:

```text
Interface              IP-Address      OK? Method Status                Protocol
Serial0/3/0            10.10.10.1      YES manual up                    up
```

For R2:

```text
Interface              IP-Address      OK? Method Status                Protocol
Serial0/3/0            10.10.10.2      YES manual up                    up
```

The important result is:

```text
Status: up
Protocol: up
```

You can also check the encapsulation using:

```bash
show interfaces serial 0/3/0
```

You should see that the interface is using **HDLC encapsulation**.

---

# Step 5: Test Connectivity

From R1, ping R2:

```bash
ping 10.10.10.2
```

A successful result should look similar to:

```text
!!!!!
```

From R2, ping R1:

```bash
ping 10.10.10.1
```

If the ping is successful, the HDLC serial connection is working correctly.

---

# Important Commands

## Configure the Serial Interface

```bash
interface serial 0/3/0
```

## Assign an IP Address

```bash
ip address 10.10.10.1 255.255.255.252
```

## Enable the Interface

```bash
no shutdown
```

## Configure HDLC

```bash
encapsulation hdlc
```

## Configure Clock Rate on the DCE Side

```bash
clock rate 64000
```

## Check Interface Status

```bash
show ip interface brief
```

## Check HDLC Encapsulation

```bash
show interfaces serial 0/3/0
```

## Test Connectivity

```bash
ping 10.10.10.2
```

---

# Conclusion

In this lab, two Cisco 2911 routers were connected using a **point-to-point serial link**. The routers used the **10.10.10.0/30 network**, with R1 configured as **10.10.10.1** and R2 configured as **10.10.10.2**.

The serial connection used **Cisco HDLC**, which is the **default encapsulation protocol on Cisco serial interfaces**. After configuring the IP addresses, enabling the interfaces, and setting a clock rate on the DCE side, connectivity was successfully tested using the `ping` command.
