# NETPRACTICE
[My solution](https://github.com/elsayedamine/NETPRACTICE) and basic explanation on NETPRACTICE and networking basics.<br>

I created this tutorial because the original project has flaws—you can solve it incorrectly, yet still get marked as correct. Most other tutorials exploit these flaws to simplify the solution, but this one sticks to proper networking logic.

## Contents
- [Basics](https://github.com/elsayedamine/NETPRACTICE#basics)
  - [Masks](https://github.com/elsayedamine/NETPRACTICE#masks)
  - [Switches](https://github.com/elsayedamine/NETPRACTICE#switches)
  - [Routers](https://github.com/elsayedamine/NETPRACTICE#routers)
  - [Routing Tables](https://github.com/elsayedamine/NETPRACTICE#routing-tables)
  - [Network](https://github.com/elsayedamine/NETPRACTICE#network)
- [Levels](https://github.com/elsayedamine/NETPRACTICE#levels)
  - [Level 1](https://github.com/elsayedamine/NETPRACTICE#level-1)
  - [Level 2](https://github.com/elsayedamine/NETPRACTICE#level-2)
  - [Level 3](https://github.com/elsayedamine/NETPRACTICE#level-3)
  - [Level 4](https://github.com/elsayedamine/NETPRACTICE#level-4)
  - [Level 5](https://github.com/elsayedamine/NETPRACTICE#level-5)
  - [Level 6](https://github.com/elsayedamine/NETPRACTICE#level-6)
  - [Level 7](https://github.com/elsayedamine/NETPRACTICE#level-7)
  - [Level 8](https://github.com/elsayedamine/NETPRACTICE#level-8)
  - [Level 9](https://github.com/elsayedamine/NETPRACTICE#level-9)
  - [Level 10](https://github.com/elsayedamine/NETPRACTICE#level-10)


## Basics

This project uses only IPv4 — IPv6 is not relevant here.

An IPv4 address is a 32-bit number divided into four 8-bit blocks (octets).  
Example:  
`192.168.100.1` → `11000000.10101000.01100100.00000001`  
Each block ranges from `0` to `255`.

The same structure applies to the network mask:  
`255.255.255.0` → `11111111.11111111.11111111.00000000`  
A key rule for masks: once a `0` appears in the binary form, all bits that follow must also be `0`.  
That means only these values are allowed in any mask block:

- `255` (`11111111`)
- `254` (`11111110`)
- `252` (`11111100`)
- `248` (`11111000`)
- `240` (`11110000`)
- `224` (`11100000`)
- `192` (`11000000`)
- `128` (`10000000`)
- `0`   (`00000000`)

So `255.255.255.0` is valid, while `255.255.128.128` is **not** — it violates the rule.
To send packets between two IP addresses, they must either be part of the same network, or be connected through a router that belongs to both subnets.

[Back to Contents](https://github.com/elsayedamine/NETPRACTICE#contents)

## Masks

The **mask** (also called network mask or subnet mask) determines which IP addresses belong to the same subnet.

There are two ways to represent a mask:

- **Dot-decimal notation**: `255.255.255.0`
- **CIDR (Classless Inter-Domain Routing)**: `/24`

The more usable IP addresses you want per subnet, the fewer subnets you can create from a given IP range.  
This table provides a helpful reference:

| CIDR | Dot-decimal        | IPs per subnet | Usable IPs | Subnets |
|:----:|:------------------:|:--------------:|:----------:|:-------:|
| /32  | 255.255.255.255    | 1              | 0          | 256     |
| /31  | 255.255.255.254    | 2              | 0          | 128     |
| /30  | 255.255.255.252    | 4              | 2          | 64      |
| /29  | 255.255.255.248    | 8              | 6          | 32      |
| /28  | 255.255.255.240    | 16             | 14         | 16      |
| /27  | 255.255.255.224    | 32             | 30         | 8       |
| /26  | 255.255.255.192    | 64             | 62         | 4       |
| /25  | 255.255.255.128    | 128            | 126        | 2       |
| /24  | 255.255.255.0      | 256            | 254        | 1       |

The number of **usable** IPs is always 2 less than the total number, because:

- The first address is the **network address**.
- The last is the **broadcast address**.

Example for `255.255.255.252`:

- Network: `190.3.2.252`  
- Broadcast: `190.3.2.255`  
- Usable: `190.3.2.253`, `190.3.2.254`

[Back to Contents](https://github.com/elsayedamine/NETPRACTICE#contents)


## Switches

A switch will enable you to connect more than two devices to the same network.<br>
Its only purpose is to distribute packages to its network.<br>
To see a working example, you can take a look at [Level 3](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level3.png).<br>

## Routers

As previously mentioned a router is an interface which enables communication between different networks.<br>
A router has the ability to be part of multiple networks, in Netpractice this is visualized by the so called `Interface`.<br>
If routers and switches are still magic to you, I suggest looking deeper [into it](https://www.youtube.com/watch?v=Vc16CCAAz7Q) yourself, as their basic understanding is crucial to succeed in this project.

[back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)

## Network

And now to connect all of the above mentioned topics.<br>
In order to have a functioning network, you now need to apply all of the parts talked about earlier.<br>
If there should be a working connection in a network, the devices somehow need to be connected, either directly or with the help of routers which are part of both networks.

Now you may ask, how do I know if two devices are part of the same network?<br>
For this you need to combine the IP-address and the mask of the devices in order to get the network-adress, that device is part of.<br>
By combining I mean, doing a bit-by-bit-AND-opperation.<br>
For that we first need to translate the IP and the mask to binary.<br>
i.e.:<br>
IP: `192.168.100.1` in binary: `11000000.10101000.1100100.00000001`<br>
MASK: `255.255.255.0` in binary: `11111111.11111111.11111111.00000000`<br>
Now you just combine the two bit by bit, if both bits are a `1` the corresponding bit of the network-address is `1`, in any other case the corresponding bit is `0`.

By doing that to the mentioned example, you should get the network-address of<br>`11000000.10101000.1100100.00000000` in binary or `192.168.100.0` in dot-decimal.<br>
[back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)

## Levels

Here are all the solutions for all 10 Levels.<br>

---

### Level 1

<details>
  <summary>show</summary>
  ![Level 1](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level1.png)

  [back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)

</details>

---

### Level 2

<details>
  <summary>show</summary>
  ![Level 2](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level2.png)

  [back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)

</details>

---

### Level 3

<details>
  <summary>show</summary>
  ![Level 3](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level3.png)

  [back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)

</details>

---

### Level 4

<details>
  <summary>show</summary>
  ![Level 4](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level4.png)

  [back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)

</details>

---

### Level 5

<details>
  <summary>show</summary>
  ![Level 5](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level5.png)

  [back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)

</details>

---

### Level 6

<details>
  <summary>show</summary>
  ![Level 6](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level6.png)

  [back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)

</details>

---

### Level 7

<details>
  <summary>show</summary>
  ![Level 7](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level7.png)

  [back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)
</details>

---

### Level 8

<details>
  <summary>show</summary>
  ![Level 8](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level8.png)

  [back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)
</details>

---

### Level 9

<details>
  <summary>show</summary>
  ![Level 9](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level9.png)

[back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)

</details>

---

### Level 10

<details>
  <summary>show</summary>
  ![Level 10](https://github.com/elsayedamine/NETPRACTICE/blob/main/my_solutions/screenshots_solutions/Level10.png)
</details


[back to contents](https://github.com/elsayedamine/NETPRACTICE#contents)
