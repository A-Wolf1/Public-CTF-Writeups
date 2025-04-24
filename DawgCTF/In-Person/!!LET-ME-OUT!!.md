# !!LET ME OUT!!

- Challenge Author: LMN1460
- DawgCTF 2025

## Prompt

I left some really REALLY important screenshots on my super-secret storage device, but now I can't find it! I know it's on the wifi of my super-secret router, but forgot the super-secret password. Got any ideas for cracking open this network and breaking those secrets out?

(Note: the router in question broadcasts the wifi network "DawgCTF_challenge_router". If your wireless card doesn't support the mode required for this challenge, there is a Kali box in the front in the room that you can use. You will however have to tell us how you want to use it first!)

## Determining Attack Method
* The first thing I did was look at the current wifi networks in the room, I was able to identify the network and see that it had WPA-PSK authentication and the channel that it was running on. I used an app on my phone but `airodump-ng` could be used to achieve the same thing.
* What tipped me off to the method of getting into the network was the mention of the "mode required for this challenge" I immediately thought of needing to use an adapter capable of "monitor" mode. This essentially allows the adapter to capture traffic on a channel without being connected. With a monitor-mode capable adapter you can preform a de-auth attack and capture handshakes. This is a good powerpoint explaining the protocols: https://owasp.org/www-chapter-dorset/assets/presentations/2020-01/OWASP-wlans.pdf

## Solution
* Enable monitor mode `sudo airmon-ng start <interface>`
* Find the AP `sudo airodump-ng <interface>` - note the channel and MAC if not identified already
* Begin capturing `sudo airodump-ng --bssid <AP-MAC-ADDRESS> -c <channel> -w capture <interface>` (You don't need to specify SSID or MAC but in a congested area with multiple SSIDs operating on the same channel its good to rule out extraneous data)
* In a separate terminal instance kick clients off by spoofing deauthentication packets, this forces the existing clients connected to re-initiate a handshake that you will be able to capture. `sudo aireplay-ng -0 10 -a <AP-MAC-ADDRESS> <interface>`
* There were maybe 3 other clients on the network, I'm assuming at least one dummy client was setup to stay connected just so we could capture the handshake. You will see when they reconnect and a handshake is triggered.
* Stop the capture in the first terminal which saves a `.cap` file
* Crack the handshake by brute-forcing the captured handshake containing the needed hash. `aircrack-ng -w /usr/share/wordlists/rockyou.txt -b <AP-MAC-ADDRESS> capture.cap` I used rockyou.txt and got lucky and found the passphrase in a few minutes. Some sort of hint to the wordlist that should be used in the prompt would've been nice though. I was also ready to find the router manufacturer via MAC and figure out if they had a default password generation scheme to brute force. 
* Now that you have the passphrase connect to the network.
* A simple NMAP scan with common ports on the subnet reveals:
    - Router with Telnet and HTTP open
    - A unidentified host with SSH and HTTP open
    - A few other hosts, likely the dummy client or other people doing the challenge.
* The unidentified host turns out to have a basic apache2 web file-share. Lot's of silly files to be seen, but a little bit of digging leads you to leaked screenshots of a signal conversation, *how suspicious*, anyways a password was shared in plaintext in the convo and that was the flag. 

![signal screenshot containing flag](https://github.com/A-Wolf1/CTF-Writeups/blob/main/DawgCTF/In-Person/Screenshot_20250416_162640_Signal.png)

