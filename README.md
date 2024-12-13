
<img src="https://i.imgur.com/wURMIsq.jpeg" />

# osTicket Prerequisites and Installation
This project demonstrates the process of setting up a ticketing system from scratch using osTicket on a Windows 10 virtual machine (VM) in Azure, showcasing technical proficiency in VM management, web server configuration, and PHP/MySQL integration. Follow along as I walk through each step, including the creation of the VM, installation of necessary software, and configuration of services, to set up a fully functional osTicket system. 

📌!!!IMPORTANT!!!Whenever installing is mentioned I am refering to installing the files in this drive [here.](https://drive.google.com/drive/u/1/)🫡

<h2>Tools & Technology Used</h2>

- Microsoft Azure 

- Virtual Machines

- RDP

- Internet Information Services [IIS]

- MySQL

<h2>Key Objectives:</h2>

- Web Server Configuration: Set up IIS (Internet Information Services) on the VM, enabling CGI and installing necessary PHP extensions to support osTicket.

- PHP and Database Setup: Install and configure PHP for the web server, along with setting up MySQL and using HeidiSQL to create the osTicket database.

- osTicket Installation: Install and configure the osTicket ticketing system, including file extraction, database connection, and basic application setup.

- Security and Permissions: Implement proper file permissions and remove setup files to ensure a secure environment.

- System Functionality: Complete the osTicket setup for both end-users and help desk agents, making it fully operational and accessible via a web interface.

<h2>Prerequisites</h2>

- An active Microsoft Azure Subscription

- Installation files [here.](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)

- Microsoft RDP: If on MAC go to APP Store and download Microsoft RDP

# Project Overview
<h2>Step 1: Create a Resource Group</h2>

<p>This will serve as a container of sorts (like a folder) that will hold our resources (Virtual Machines)</p>

- Go to Azure Portal

![image](https://github.com/user-attachments/assets/6f75e551-4d66-4af6-a20e-8a1f6fa831fe)

- Go to Resource Group

![image](https://github.com/user-attachments/assets/37506426-1785-44af-8dff-d2fbf4735d20)

- Create Resource Group

![image](https://github.com/user-attachments/assets/d1571f43-284a-4721-b0ad-1d170b33273e)

- Name the Resource Group

![image](https://github.com/user-attachments/assets/c45b31c1-83c8-4e6e-8e25-20b0be0eb104)

- Review and Create Resource Group

![image](https://github.com/user-attachments/assets/b98e48a6-a504-44df-899a-2b91a9354f7e)

- Create Resource Group

![image](https://github.com/user-attachments/assets/cfa87af7-f3c9-44aa-8912-4d34c05ed2b8)

- Resource Group Succesfully created

![image](https://github.com/user-attachments/assets/c2859c23-b3cb-4c60-89ca-c436937415ed)

<H2>Step 2: Creating Resource (Virtual Machine)</H2>

- Return to the Azure Portal and find the "Virtual Machines" option (You can search it in the searchbar if you cant find the option in the dashboard) 

![image](https://github.com/user-attachments/assets/37ac9f7a-e86c-44b7-aa37-d125469a692f)

- Create a virtual machine resource 

![image](https://github.com/user-attachments/assets/64829dcf-3278-4353-a19d-dc6f9425a77f)

- Assign the VM to the Resource Group that was created

![image](https://github.com/user-attachments/assets/d101a9e4-3db9-4de2-b485-556884d23b03)

- Fill out these details:<br> 
-Virtual Machine Name<br>
-Region [!!IMPORTANT!! Make sure that the region used to create the resource group is the same as the region as the VM you are creating, might run into issues otherwise] <br>
-Image [we are going to make a Windows 10 VM so make sure to select the Windows 10 pro option for image]<br>

![image](https://github.com/user-attachments/assets/6d08279c-cba8-4fa2-94d2-1f180a82f7e9)

- For optimal performance I will use 2cpus as the standard size<br>

![image](https://github.com/user-attachments/assets/08cfa758-8454-4343-9665-f5081ebfdd80)

- Create Username and password 

![image](https://github.com/user-attachments/assets/028d853e-63a4-4d23-938e-b3c39daa1d01)

Confirm Licensing 

![image](https://github.com/user-attachments/assets/d25e7c66-a950-461c-a7fb-6e1109460123)

- Review and Create 

![image](https://github.com/user-attachments/assets/bdce6266-ec36-43a7-9aaa-9ec34b2c6a10)

![image](https://github.com/user-attachments/assets/dd270697-8d60-4b08-944e-e45ddae3e3ca)

- Virtual Machine (Windows 10 Pro) Successfully Created.<br>

<h2>Step 3: Use RDP to log into the windows vm </h2>

- Return to the Virtual Machine Dashboard in the Azure portal

![image](https://github.com/user-attachments/assets/a2e686dc-d035-432b-a079-18927560bc76)

- Jot down the Public IP adresses of the Windows VM 

![image](https://github.com/user-attachments/assets/1a8e4a73-f175-42fb-bb68-6ba3ab1b18ba)

- If on Windows press Windows key -> Open RDP If on MAC download RDP program in APP store and put in the IP adress of the Windows VM 

![image](https://github.com/user-attachments/assets/5f159faa-a725-4e26-b101-de3f7121278e)

- Enter the Log in credentials and log in to the machine 

![image](https://github.com/user-attachments/assets/ea9d83e9-20e4-4f72-860a-85defe141e06)

<h2>Step 4: Install and enable IIS wtih CGI (Internet Information Services| Windows web server ) </h2>

- Navigate to to the Control Panel -> Programs -> Turn Windows Features On or Off -> Internet Information Services

- Now Enable CGI: World Wide Web Services -> Application Development -> CGI 

![image](https://github.com/user-attachments/assets/ef0e4a86-1e22-4d5f-abf0-5124d2968245)

- 🎉 Awesome! By enabling IIS, you can now host web applications directly on your machine. Enabling CGI takes it a step further, allowing your web app to dynamically adapt based on user interactions and database inputs. This sets the stage perfectly for the mighty ticketing system to establish its roots!

<H2>Step 5: Enable all Common HTTP Features  (Virtual Machine)</H2>  

- Navigate to the Common HTTP Features and enable all features. Then apply the changes
![image](https://github.com/user-attachments/assets/2e0624ed-5640-4258-ac22-4f8341ce777d)
- Press ok to apply the changes we made 
![image](https://github.com/user-attachments/assets/df2d20e5-231b-4a70-9ead-262a4f2dfed3)


<H2>Step 6: Test Web Server Installation </H2>

- Type the loopback IP (127.0.0.1) in the internet browser  to see if the web server is up and running this page should be showing 
![image](https://github.com/user-attachments/assets/6a2b24c9-2ab6-44fa-9bc8-33b32b76eebc)

<H2>Step 7: Set up PHP </H2>

- Install PHP manager for IIS Setup:  <br/>
<img src="https://imgur.com/RuAUGw1.png" height="80%" width="80%" alt="Setting Up in Azure"/>

- This sets up PHP, the language responsible with communnicating with the database,formating and displaying that data for us. This means that PHP is responsible for keepign track of the tickets, permissions etc. A.K.A its really important   

- Install IIS URL Rewrite Module:  

<img src="https://imgur.com/465p9DH.png" height="80%" width="80%" alt="Setting Up in Azure"/>

- Create a PHP directory on the C drive

<img src="https://imgur.com/CEsoJp6.png" height="80%" width="80%" alt="Setting Up in Azure"/>

- Download PHP and extract the zip file in the PHP directory we just made:  

<img src="https://imgur.com/LoYw0cZ.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<H2>Step 8: Download Microsodt Visual C++ </H2>

<img src="https://imgur.com/SocF97p.png" height="80%" width="80%" alt="Setting Up in Azure"/>


<H2>Step 9: Download MYSQL  </H2>

<img src="https://imgur.com/dFdQagT.png" height="80%" width="80%" alt="Setting Up in Azure"/>

  - This is the database will hold all of the information we need for the ticketing system

- Setup the login credentials I'll write them down just so I remember, since this is only a project. Do not write passwords down in real life:  <br/>
<img src="https://imgur.com/SeJVW6M.png" height="80%" width="80%" alt="Setting Up in Azure"/>

- Write them down in case you forget these creditenials are important. This is only a project it is bad practice to have this written down, DO NOT DO THIS IN REAL LIFE

<H2>Step 11: Open IIS as an admin</H2> 
<img src="https://imgur.com/gFmrka6.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<H2>Navigate to PHP Manager -> register new PHP version -> select file shown</H2>

<img src="https://imgur.com/nlD4F1L.png" height="80%" width="80%" alt="Setting Up in Azure"/>


<H2>Step 12: Navigate to osTicket Home -> Manage Server(On the right side ) -> Restart </H2>
<img src="https://imgur.com/F83Qw2a.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<H2>Step 13: Download osTicket -> copy the upload file to the wwwroot file to the inetpub directory</H2>
<img src="https://imgur.com/op4Cs2g.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<h2>Step 14: Rename upload file to osTicket </h2>  
<img src="https://imgur.com/ZBLsJsB.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<h2> Step 15: Reload IIS -> Manage Server(On the right side ) -> Restart the server -> then click Browse *80 (http) on the right side </h2>
<img src="https://imgur.com/JnqQOJD.png" height="80%" width="80%" alt="Setting Up in Azure"/>

This page should open: 
<img src="https://imgur.com/J4E020x.png" height="80%" width="80%" alt="Setting Up in Azure"/>

- 🎉 Awesome we have got the osTicket webpage up and running now lets configure it so we can use it

<h2>Step 16: Enable recommended extensions</h2>
- Notice that some extensions aren't enabled. The site might not run as you expext if you dont setup these extensions. 

- Navigate to Sites -> Default Web Site -> osTicket Click PHP Manager -> Enable or disable an extension -> Enable php_imap.dll, php_intl.dll, and php_opcache.dll 

<img src="https://imgur.com/ZJCdcDV.png" height="80%" width="80%" alt="Setting Up in Azure"/>

- The webpage should have those spots checkmarked now

<img src="https://imgur.com/yZbaGml.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<h2>Step 17: Browse in File Explorer to the C drive -> osTicket -> Include -> ost-sampleconfig.php -> Remove "sample" from the name </h2>Next browse in file explorer to C drive> osTicket> include> ost-sampleconfig.php and remove the "sample" from the name:  <br/>

<img src="https://imgur.com/k6cfJaY.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<h2> Step 18: Right-click on ost-config.php -> Properties -> Security -> Advanced> Disable Inheritance --> Remove all inherited permissions from this object </h2>

<img src="https://imgur.com/G154DIx.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<h2> Step 19: Click on the add buton to add permissions to the file> Select a principle -> type "everyone" -> Check -> OK -> check all permissions> OK> apply -> OK </h2>
<img src="https://imgur.com/clvmCHq.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<H2> Step 20: Hit continue on the osTicket web page in the browser and fill out the information </H2>

<img src="https://imgur.com/dYLO5Ot.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<h2> Step 21: Before database set up Connect the database using HeidiSQL. Install HeidiSQL from setup links  </h2>

<img src="https://imgur.com/tyyovzJ.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<h2>Step 22: In HeidiSQL click New -> Username = root -> Password = mySQL password from mySQL setup -> Open </h2>

<img src="https://imgur.com/xoW0TMX.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<h2>Step 23: In HeidiSQL right click Unnamed -> Create -> New Database> Name it osTicket -> OK. 
 Then continue to fill out the database portion of osTicket setup. Click Install Now when done</h2>

<H2>Last steps:  Clean up go to C driveV-> inetpubV-> wwwrootV-> osTicket and look for the setup file and delete it

Then go to C drive -> inetpub -> wwwroot -> osTicket -> include right click on ost-config.php -> Properties -> Security -> Advanced -> Select Everyone and click edit -> only leave Read & Execute and Read checked -> then apply settings </H2>
<img src="https://imgur.com/o4GB231.png" height="80%" width="80%" alt="Setting Up in Azure"/>

  # 🎉Congratulations

<h2>We Have Successfully:</h2>

<h2>osTicket Installed!</h2>

- Deployed Virtual Machines (VMs) on Microsoft Azure

- Configured a web server with IIS to host ticketing system

- Installed PHP and its required extensions to facilitate communication with the database, enabling dynamic formatting and display of data.

- Created and configured a MySQL database (with HeidiSQL as a management tool) to store crucial data such as users, permissions, SLAs, and ticket information.

  - Installed and configured a web hosted ticketing system - osTicket 

# That Concludes this lab. In the next lab we will configure users, permsissions, access in the ticketing system and SLA's  <img src="https://media.giphy.com/media/hvRJCLFzcasrR4ia7z/giphy.gif" width="30px"/>

