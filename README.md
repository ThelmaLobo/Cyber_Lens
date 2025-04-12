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

From the above image we understand Apache Tika 1.17 is running on the target machine. Apart from that, we havent found anything fruitful on this website. We need to explore if we can find any exploits on this Tika Server. For that we do the following using Metasploit as below - : <br/>
<img width="737" alt="Screenshot 2025-04-08 at 11 03 53 pm" src="https://github.com/user-attachments/assets/dbfbf341-10c8-4593-bf96-ab573fdbdac3" />
<img width="750" alt="Screenshot 2025-04-08 at 11 04 51 pm" src="https://github.com/user-attachments/assets/15d36420-2a68-460b-9f5b-0fdb9caa9588" />

Inorder to the use that exploit, we need to execute the this command use exploit/windows/http/apache_tika_jp2_jscript and follow below steps : <br/>
<img width="942" alt="Screenshot 2025-04-08 at 11 06 38 pm" src="https://github.com/user-attachments/assets/08f51116-efb1-447b-9dd2-77b7ce46834e" />

After executing the Show Options command we can see the required options such as the RHOSTS, RPORT and TARGETURI. I had some internet issues, so couldnt take a snippet where I had executed the exploit command. Therefore, I suggest that once the ports and IP address are set, we need to execute the Exploit command which will give you a meterpreter session. Once you see the meterpreter, that means the machine has been compromised. The next step we need to escalate the privileges : <br/>
<img width="745" alt="Screenshot 2025-04-08 at 11 17 08 pm" src="https://github.com/user-attachments/assets/03dd5316-8ba9-4848-ad48-4706f8d504c4" />
<img width="745" alt="Screenshot 2025-04-08 at 11 21 23 pm" src="https://github.com/user-attachments/assets/00a6a96c-fa09-4bb4-81ee-cd49830ea5d9" />

We can use a background to exit the meterpreter session and a module called multi/recon/local_exploit_suggester to perform enumeration. We need to supply the session number : </br>
<img width="726" alt="Screenshot 2025-04-12 at 1 13 25 pm" src="https://github.com/user-attachments/assets/2739de3c-1fd1-4248-a95a-3af3ad33d5a9" />
<img width="760" alt="Screenshot 2025-04-08 at 11 34 23 pm" src="https://github.com/user-attachments/assets/a171502c-9727-436a-8153-4091f218a42b" />

For suppling the session number, we exceute command called sessions -i : </br>
<img width="760" alt="Screenshot 2025-04-08 at 11 34 58 pm" src="https://github.com/user-attachments/assets/4757ae8e-35d8-41f4-9e91-d7e742206c40" />

As we can see the session is 1, we need to set the SESSSION to 1 as below and use run command. This run command will help us find for any vulnerabilities or security misconfigurations which will enable us to escalate the privileges. We have found couple of vulnerabilities as shown in the below screenshot : </br>
<img width="760" alt="Screenshot 2025-04-08 at 11 35 44 pm" src="https://github.com/user-attachments/assets/f58a02f2-a454-40d0-8a05-e4ce78261e3d" />

The target machine's IP address got changed as I had some issues with the internet and as a result of that, I had to re-perform this CTF again. In Try Hack Me machines, every time the page is refreshed, the IP address changes. However, you need to follow the same steps I have done below :
<img width="1079" alt="Screenshot 2025-04-08 at 11 39 36 pm" src="https://github.com/user-attachments/assets/7b93eb94-8059-4961-982d-885c281e8665" />

We start with first exploit and try to see if we can find something here : </br>
<img width="1079" alt="Screenshot 2025-04-08 at 11 40 12 pm" src="https://github.com/user-attachments/assets/c798492f-011f-4087-96f8-1207d779f32e" />

We need to execute the use command : </br>
<img width="768" alt="Screenshot 2025-04-08 at 11 43 09 pm" src="https://github.com/user-attachments/assets/da023be6-97ec-4ff3-85e5-d458944f344d" />
<img width="768" alt="Screenshot 2025-04-08 at 11 43 38 pm" src="https://github.com/user-attachments/assets/a2d5dc8d-d7b1-44ea-b6e9-ee9d29cf0c0c" />

Next we use the show options to list all the available. Here, we need to set the SESSION to 1 and execute the run command. We can see the NT AUTHORITY/SYSTEM that means we have successfully elvated the privileges. We need to use getid command  : </br>
<img width="768" alt="Screenshot 2025-04-09 at 9 11 59 pm" src="https://github.com/user-attachments/assets/982d8504-c027-4fea-be82-9c13dd2d2b3d" />
<img width="768" alt="Screenshot 2025-04-09 at 9 15 25 pm" src="https://github.com/user-attachments/assets/156428b7-1924-4d15-bafd-90a2ef5b7d44" />
<img width="768" alt="Screenshot 2025-04-09 at 9 16 02 pm" src="https://github.com/user-attachments/assets/85ddaf59-18ff-4e89-bd29-006cdc8449b1" />

We use the Administrator directory : </br>

<img width="768" alt="Screenshot 2025-04-09 at 9 17 44 pm" src="https://github.com/user-attachments/assets/4a31e51e-bc41-4b26-adf0-0e2a2a5e4968" />
<img width="768" alt="Screenshot 2025-04-09 at 9 18 34 pm" src="https://github.com/user-attachments/assets/ba3846d3-4453-4131-aa30-4f3bf8b00097" />

Under the Administrator we cam see a text file called admin.txt. By opening that text file using touch command, we can see the admin flag : </br>
<img width="747" alt="Screenshot 2025-04-09 at 9 19 19 pm" src="https://github.com/user-attachments/assets/dc3a536e-28a3-4f65-96d7-e203d576d891" />
<img width="747" alt="Screenshot 2025-04-09 at 9 19 51 pm" src="https://github.com/user-attachments/assets/c101156e-9c66-4a98-bf50-87b8a3fb225e" />

Next we need to find the user flag : </br>

<img width="747" alt="Screenshot 2025-04-09 at 9 22 13 pm" src="https://github.com/user-attachments/assets/b6779b74-5b0d-4616-bdfd-833a287bf433" />
<img width="747" alt="Screenshot 2025-04-09 at 9 23 14 pm" src="https://github.com/user-attachments/assets/c6d0eac4-0529-462e-ae25-564a91d4cc3e" />

Here, we can see the user.txt file. We are close to getting our second flag : </br>
<img width="747" alt="Screenshot 2025-04-09 at 9 24 55 pm" src="https://github.com/user-attachments/assets/a239c7ac-10e2-4f44-9f69-91e761b231a4" />

We need to open that find using the touch command : </br>
<img width="747" alt="Screenshot 2025-04-09 at 9 25 24 pm" src="https://github.com/user-attachments/assets/d763a402-59a5-46f9-b54d-02a35e45f7bd" />

Yay!!! We have got both the flags and this our final output : </br>
<img width="747" alt="Screenshot 2025-04-09 at 9 27 00 pm" src="https://github.com/user-attachments/assets/1505d0f0-39de-4fe3-97a8-343e2a4e8971" />

