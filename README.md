<h2>Cyber Lens </h2>

<h2>Description</h2>

<img width="1369" alt="Screenshot 2025-04-08 at 10 29 12 pm" src="https://github.com/user-attachments/assets/3d17f545-3cb4-4123-b8ea-f62b171557a0" />

<h2>Environments Used </h2>

- <b>  Ubuntu 20.4.6 LTS </b>
- <b> Target Machine (Provided by Try Hack Me) </b> 

<h2>Program walk-through:</h2>


<p align="center">
  
<p align="center">
  
I am using the Try Hack Me VM to perform this CTF. As shown below, the IP address of the target machine is 10.10.140.147 : <br/>
<img width="1340" alt="Screenshot 2025-04-08 at 10 29 40 pm" src="https://github.com/user-attachments/assets/361055a1-744a-45ad-876f-211edfa88a47" />

We need to ping this machine just to see if communication can be established between both the machines or not. Once, we are able to ping the target machine we need to use nmap command to check for open ports on the target machine. This is the initial step for enumeration. Here, we can see that multiple ports are open out of which we are interested in port 80 i.e. http : <br/>
<img width="691" alt="Screenshot 2025-04-08 at 10 34 44 pm" src="https://github.com/user-attachments/assets/e0ab35d9-9e3e-4db8-a696-0c2add7e030a" />

We will be going on to 10.10.140.147 in the browser. Here we can the web page for cyber lens : <br/>  
<img width="886" alt="Screenshot 2025-04-08 at 10 37 46 pm" src="https://github.com/user-attachments/assets/85bffb5e-eaa7-4ebd-8bf7-cc4d80c972c2" />
<img width="886" alt="Screenshot 2025-04-08 at 10 38 02 pm" src="https://github.com/user-attachments/assets/01cf5ea1-1a33-4d98-8254-839be5037667" />


We will be searching for flags in this web page. Lets see if we find any useful information here. I will be looking into the View Source of this page. Here we found the port number 61777. I have used this port number and discovered a web page as below. We can see Apache 1.17 Tika Server: <br/>
<img width="1060" alt="Screenshot 2025-04-08 at 10 58 38 pm" src="https://github.com/user-attachments/assets/6ddc95a4-619b-4ec1-be45-8b92c88c1a7d" />

<img width="1060" alt="Screenshot 2025-04-08 at 10 57 33 pm" src="https://github.com/user-attachments/assets/d87d549f-6170-4de5-bd1d-7b6fd04e80e3" />
