
# Project MyNGFW Agent

<br><br>
<a href="https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=FestiveProject.drawio#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1D9WyrCkAx0tYXvUey82syTqF54u-n72T%26export%3Ddownload">
<img src="/img/NetworkTopology.svg">
</a>
<br><br>

### The Network
A Virtual Network consists of a victim machine and a Palo Alto Virtual NGFW running on Azure. The Palo Alto NGFW has two zones – an Internal Zone representing an internal private network and a Public Zone responsible for communicating traffic from the Internal Zone to the outside world. Traffic originating from the Internal Zone gets NATed at eth1.

The above Virtual Network is virtual peered to another Virtual Network consisting of MyNGFW Agent with a single interface eth0 that is connected to a virtual gateway with a public IP address and NATs traffic going to the internet.

The traffic from the victim machine to the internet is routed using a mix of Palo Alto Static Routes, Azure Route Tables and the good old iptables.

The MyNGFW Agent is responsible for TLS interception (by acting as a forward proxy) and running the AI Pattern Analysis Engine. The Palo Alto NGFW has a decryption profile that allows it to view encrypted traffic in plain text. The Palo Alto NGFW is then responsible for running the Advanced Wildfire and Advanced URL Filtering features on the plain text traffic.

Advanced Wildfire – a feature that essentially detonates every file passing through the network in a sandbox (in real-time) and cuts off the file if that file is determined malicious.
<br>Advanced URL Filtering – similar to Wildfire, but instead of files, it detonates URL web pages. 

The premise of this project began with the question:
<br>&emsp;&emsp;&emsp;&emsp;“What if an adversary bypasses system-level protections”

The MyNGFW Agent is an agent that aims to solve this problem by detecting any attack at the network layer. We do this by translating attack TTPs to how they would look like over the network, and use that pattern intelligence to train the AI Pattern Analysis Engine.

The AI Pattern Analysis Engine powered by Llama 3.2 inspects traffic passing through the MyNGFW Agent and detects any cyber attacks. This is complemented by the Palo Alto detonation feature that detects any advanced malware using basic dynamic analysis. 

At the completion of the project, I’ll simulate five prominent APTs carrying out multi-stage attacks on the victim machine and we shall see the MyNGFW Agent detect these attacks.

Timeline of the Project
<br>Phase I&emsp;&emsp;&emsp; &nbsp;The Network - _Completed_	
<br>Phase II&emsp;&emsp;&emsp; Setup TLS interception, the Decryption Profile, Wildfire & Advanced URL Filtering - _Completed_
<br>Phase III&emsp;&emsp;&emsp;Develop the AI Pattern Analysis Engine - _Ongoing_
