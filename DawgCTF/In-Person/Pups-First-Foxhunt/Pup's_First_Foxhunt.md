# Pup's First Foxhunt

- Challenge Author: LMN1460
- DawgCTF 2025

## Prompt

Somewhere in the (publicly accessible!) areas of Commons will be a person walking around with my Flipper Zero. This device is the "fox" you will have to hunt by tracking its Bluetooth signal strength! Its name is "Flipper End4tre3" and MAC address is 80:E1:27:65:86:ΑΑ. Τo capture the fox you must ask the person you think is carrying it "are you the Bluetooth fox?". Bring it back to the DawgCTF rooms to claim your flag! The fox holder will be wearing or carrying a CyberDawgs CDE shirt, so please don't harass random students. Good luck, and happy hunting! 

Hint: Something about the app nRF connect

## My thought process / What I did
- This challenge ended up being relatively self explanatory. There is a bluetooth device somewhere, and it's broadcasting we just need to find it.
- The issue is this area of the school is a very well trafficked  area with a high amount of bluetooth device density. Scans in different places in the building yield 50 to 150 devices in range at a given time.
- I knew that I needed to be able to view bluetooth devices and filter or search for this specific device ID that I knew. I got 3 different apps and even paid $3 on one app to filter by MAC :dead:
- Then I actually realized there was a hint and got the app `nRF Connect` this made it super easy to filter by MAC.
- That said it didn't help too much and I didn't see anything until I was directly in the room with the fox. Theoretically the signal strength should be able to help you locate the device easier. And if the fox wasn't in plain site it would've caused me to search harder.
## The Solution / TLDR
- Get `nRF Connect` filter by MAC or Name to locate the device among the multitude of other devices.
- Once in range it'll give you a signal strength in -dB that can help you locate it's location.
