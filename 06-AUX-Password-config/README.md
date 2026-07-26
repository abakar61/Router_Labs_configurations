# 🔐 AUX Password Configuration on Cisco Router

## Description

In a real-world Cisco network, network administrators must secure every method used to access a router. One of these methods is the **Auxiliary (AUX) port**, which was traditionally used for remote management through a modem.

Configuring an **AUX password** ensures that only authorized users can access the router through the AUX port. Although the AUX port is rarely used in modern networks, understanding its configuration remains an important CCNA skill.

---

## Objective

Learn how to configure an AUX password on a Cisco router to secure access through the Auxiliary (AUX) port.

---

## Company Scenario

You have recently joined **TechSolutions Ltd.** as a **Junior Network Administrator**.

Your company maintains Cisco routers that support multiple management methods. As part of the organization's security policy, every management interface must be protected with a password.

Your manager asks you to configure an AUX password on the router, verify that password authentication is enabled, and save the configuration.

Your task is to complete the following practice projects.

---

## What is an AUX Password?

An **AUX password** is a password that protects access to a Cisco router through its **Auxiliary (AUX) port**.

The AUX port is a management port that was traditionally used to remotely access a router through a **modem connected to a telephone line**. When a password is configured and the **login** command is enabled, users must enter the correct password before accessing the router.

---

## Syntax

```bash
line aux 0
password PASSWORD
login
```

### Example

```bash
Router(config)# line aux 0

Router(config-line)# password Cisco123

Router(config-line)# login
```

---

# Project 1 – Configure an AUX Password

### Task

Secure the AUX port by configuring a password and enabling password authentication.

### Commands

```bash
enable

configure terminal

line aux 0

password Cisco123

login

end

copy running-config startup-config
```

### Expected Output

The AUX line is protected with a password, and users connecting through the AUX port must authenticate before accessing the router.

---

# Project 2 – Verify the AUX Configuration

### Task

Verify that the AUX password has been configured correctly.

### Commands

```bash
show running-config

show running-config | section line aux

show startup-config
```

### Expected Output

```text
line aux 0
 password Cisco123
 login
```

---

# 🌐 Packet Tracer Topology

```text
                Console Cable
     +-------------------------------+
     |                               |
+-----------+                 +---------------+
|    PC1    |-----------------|   Router R1   |
| (Admin)   |                 |               |
+-----------+                 +---------------+
```

**Note:** Packet Tracer does **not** simulate modem connections through the AUX port. Therefore, you use the **Console cable** to configure the AUX password from the router CLI. The AUX password protects the AUX line configuration, even though you are not connecting through the AUX port in Packet Tracer.

---

## 🎯 Packet Tracer Tasks

### Task 1 – Configure the AUX Password

Requirements:

- Enter privileged EXEC mode.
- Enter global configuration mode.
- Configure the AUX line.
- Set the password to **Cisco123**.
- Enable password authentication.
- Save the configuration.

Commands:

```bash
enable

configure terminal

line aux 0

password Cisco123

login

end

copy running-config startup-config
```

---

### Task 2 – Verify the Configuration

Requirements:

- Display the running configuration.
- Verify that the AUX line has a password.
- Verify that the login command is enabled.

Commands:

```bash
show running-config

show running-config | section line aux
```

---

## Verification Commands

### Display the Running Configuration

```bash
show running-config
```

---

### Display Only the AUX Configuration

```bash
show running-config | section line aux
```

---

### Verify the Saved Configuration

```bash
show startup-config
```

---

## Expected Result

After configuration:

- ✅ The AUX port is protected with a password.
- ✅ Password authentication is enabled using the `login` command.
- ✅ The configuration is saved permanently.
- ✅ Unauthorized users cannot access the router through the AUX port without the correct password.

---

## What I Learned

- Configure the AUX line using `line aux 0`.
- Set an AUX password using the `password` command.
- Enable password verification using the `login` command.
- Save the configuration using `copy running-config startup-config`.
- Verify the AUX configuration using `show running-config`.
- Understand that the AUX port was traditionally used for remote management through a modem.
- Learn a fundamental Cisco IOS security configuration commonly covered in CCNA.