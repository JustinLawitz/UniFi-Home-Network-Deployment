# UniFi-Home-Network-Deployment

## The Problem:

 About a year ago we upgraded to google fiber as it was installed in our area and boasted speeds 10 times faster than Spectrum. While the internet worked extremely well when either connected through ethernet directly to the router, or in the general vicinity of the router or 1 access point (AP), it worked perfectly. But on the opposite side of the house from the router, and just out of range of the AP, the internet connection was either extremely weak or offline altogether.
 
## Old hardware:

Our old router was the Google - Nest Wi-fi Pro (Figure 1) that came with changing to google fiber. The interesting thing about this router is that they can act as both the router and AP using something called bridge mode. Bridge mode essentially turns off one of the Google Nests routing functions like NAT (Network Address Translation) and DHCP (Dynamic Host Configuration Protocol) and instead uses it as a pass-through AP. For instance, in our home network we had one acting as the router, and another in the living room acting as an AP. While this would normally be fine, in our case we only had 2 Google Nests and needed 1-2 more to get full coverage throughout the house, and these specific routers are around $300 each. Another problem is it is hard to configure advanced network features like port forwarding on the Nest Pro which I plan to use in future projects. 

 <img width="975" height="731" alt="image" src="https://github.com/user-attachments/assets/aa38f696-90eb-4b0f-9c73-8c5af2e35c35" />
Figure 1: Google - Nest Wi-fi Pro

## New hardware:

In our case, the best solution was to completely re-do the home network with a new router and APs. The router I decided on was the Unifi Dream Machine due to recommendation, and the fact that it acts as the router, firewall, switch, and network controller all in one package. The router itself is the same price as one Google Nest at about $300. For the APs I decided on the Unifi U6+ which were about $130 each; To get full coverage of the house I got 3 APs. The one slight issue with the U6+ APs was that the only way to power the AP was through one PoE ethernet port, but the Dream machine doesn’t have any PoE ports, so with some research I learned about PoE injectors and how I could use them to provide both power and connection to each AP. Figure 2 of the image is the new hardware, with the Dream Machine in the top left, U6+ APs in the top right, zip ties for wire management bottom left, PoE injectors bottom middle, and Cat5 ethernet cables bottom right. While all of the hardwares price combines is slightlt more expensive than if we bought two more Google Nests, the advantage is being able to configure advanced network options like port forwarding much easier, and expandability, meaning if we ever need more APs (if we wanted to put one on the patio for instance), they will be much cheaper than getting another Google Nest. The full list of hardware used is as follows:
1 Unifi Dream Machine
3 Unifi U6+ APs
3 Unifi PoE injectors
5 Cat5 Ethernet cables
1 100 pack of zip ties

 <img width="975" height="731" alt="image" src="https://github.com/user-attachments/assets/ff85b14d-87d9-4dee-bea3-9bf1b29412e0" />
Figure 2: New Unifi hardware

## Setup

With the new hardware bought and the old hardware removed, the first step was to setup the Unifi Dream Machine router. While the setup could be done through the browser and an ethernet connection or the app, I already had the app installed so I configured the router and APs that way due to being able to check connectivity throughout the house, and ease of access.

### Step 1.

The first step was to plug in the Dream machine to an outlet for power, and plug it into the Optical Network Terminal (Figure 3), which is a box that transfers the fiber optic from the street, to be compatible with ethernet. The ethernet cable to the Optical Network Terminal should go into the WAN (Wide Area Network) port on the router to provide it with internet. In this step I also connected my PC to port 1 on the router using a spare ethernet cable (Figure 4).

 <img width="975" height="731" alt="image" src="https://github.com/user-attachments/assets/993e88d3-8929-44c4-b3cb-fbe2a0569617" />
Figure 3: Optical Network Terminal

 <img width="975" height="731" alt="image" src="https://github.com/user-attachments/assets/181866e4-8740-4621-b38f-8ebdc79ec955" />
Figure 4: Connected Dream Machine

### Step 2:

The next step was to set up the router through the Unifi app. After the router was powered on and detected by the app, I set up the router’s SSID (Service Set Identifier) which is the Wi-fi network’s name and entered a password to access the Wi-fi. After the router was set up, I was able to view and edit settings, activity on the network, and more on the app and browser (Figure 5).

<img width="357" height="776" alt="image" src="https://github.com/user-attachments/assets/ddfdfa7e-70bb-4ab4-a36e-e00b66f57437" /><img width="356" height="774" alt="image" src="https://github.com/user-attachments/assets/d3fd7408-e329-44a2-9ba6-9622c2be74dd" />

Figure 5: Wi-Fi Setup, settings, and network activity

### Step 3:

After the router was online, the next step was to connect the APs. Something to note about the Unifi Dream Machine and U6+ APs is that to have an AP wirelessly connected to the router, one must be directly connected to the router using an ethernet cable. How this works is the first wired AP acts as a gateway for the other wireless APs, meaning that it provides them with configuration like which SSID to broadcast, network access, and backhaul which is the path the AP uses to send client traffic back to the main router, so on the wired AP the backhaul is the ethernet cable, and the wireless APs backhaul is a dedicated wireless link. To set this up, I used the first PoE injector and connected it to a power outlet and then used two Cat5 ethernet cables to connect it to both the router (in this case Port 2), and to the AP itself (Figure 6).

<img width="975" height="731" alt="image" src="https://github.com/user-attachments/assets/fcd8cec7-e901-4449-a4da-02885f76ac74" />
Figure 6: Wired AP

Another thing to note is that it is very important which port you use on a PoE injector to connect the router and the AP. At first, I was confused as I had connected the PoE injector to the outlet, router, and AP but the AP wasn’t powering on. With a bit more inspection I noticed the symbols on the PoE injector (Figure 7). In this case the left port was to power the AP, and the right port to provide it with access to the network. After realizing I had the ports swapped I changed them and it worked.

<img width="897" height="672" alt="image" src="https://github.com/user-attachments/assets/d890addd-c907-4c88-9bb3-8da45593a444" />
Figure 7: PoE injector symbols

### Step 4: 

After successfully connecting the PoE injector and AP, I next had to set it up in the app. After it was detected, I was able to connect and onboard it after a short update. After this update the AP was online and operational (Figure 8).

<img width="363" height="788" alt="image" src="https://github.com/user-attachments/assets/98e91e5e-33ad-404c-95b5-5eda9cc54671" /><img width="363" height="788" alt="image" src="https://github.com/user-attachments/assets/0373287e-2c0c-4011-8ee4-59c0e024e890" />

Figure 8: AP setup

### Step 5:

The setup of the wireless APs were similar, the only difference being that after the onboarding process, I disconnected it from the port to the router and brought it to the location in the house I wanted it at. Once I decided on a location, I plugged the PoE injector into a power outlet and made sure the AP was still connected to the port on the PoE injector that gave it power (Figure 9). After the AP restarted, it was wirelessly connected to the network. I did this same process again and placed one in the living room, and one in the entry way across the house. The one caveat about wireless APs is that the connection speed is about half of one that is directly wired to the router. In our case that was completely fine as the router is in the office and can be connected to my PC with an ethernet cable. Across the house is where the bedrooms are and mainly only light tasks like browsing would be needed.

<img width="975" height="731" alt="image" src="https://github.com/user-attachments/assets/ea8bac2f-56ee-48f5-b0f8-869d8240fe7c" />
Figure 9: Wireless AP

### Step 6:

 The final step in upgrading our home network was to check if the router was broadcasting both 2.4 and 5 GHz. Before getting the correct router, I got a single band Dream Machine instead of a dual band as I didn’t know the difference and the single band was cheaper. After that router arrived and I set it up, I realized some devices on the home network no longer functioned like our bird feeder that captures video of each bird for example. After a bit of research, I found that the router could only broadcast 5 GHz which offered faster speeds and less interference at a shorter range, or 2.4 GHz which offered longer range and better penetration through walls but at the cost of slower speeds. After realizing this I was able to swap the router for the dual band option. I was able to check the advanced settings in the Unifi app to confirm it was broadcasting both 5 and 2.4 GHz, and the priorly disconnected devices connected easily. I also thought the topology map of the network in the Unifi app was interesting and a good stopping point to complete my first big project and start of my home lab (Figure 10).
 
<img width="472" height="1027" alt="image" src="https://github.com/user-attachments/assets/614c1db2-c260-40a2-b5f9-4aa38f7e6a21" /><img width="474" height="1031" alt="image" src="https://github.com/user-attachments/assets/7a563345-aff8-4e4e-bc3d-06d56e021cc5" />

Figure 10: Dual band and topology
