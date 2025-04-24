# Pup's First Foxhunt

- Challenge Author: LMN1460
- DawgCTF 2025

## Prompt
There is a wifi network in **Commons 329**, however it is hidden. The first part of its identification is 02:44; can you get the whole ID?


## My thought process / What I did
- By "hidden" it can be assumed that this is a "hidden network" or a network with SSID broadcast disabled. That just means it won't have a name attached to it. Also the identifier of `02:44` looks like the start of a MAC address which is typically displayed as `:` delimited bytes
- I used an app called `WiFiman` to look at the networks around and was quickly able to find the network among the list with a MAC starting with `02:44` noting the rest of the MAC address was the flag.
- Here's a screenshot of what a hidden network looks like and you can see the MAC address displayed below

![WiFiman screenshot showing networks](https://github.com/A-Wolf1/Public-CTF-Writeups/blob/main/DawgCTF/In-Person/Hidden-Network/Screenshot_20250423_233336_WiFiman.jpg)