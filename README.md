<p align="center">
  <img src="https://i.imgur.com/rMB4Xot.png" height="80%" width="80%" alt="Ubuntu VM" alt="Traffic Examination"/>
</p>

<h1>Azure Sentinel (SIEM) - Exposing VM and Monitoring LIVE Global Attacks</h1>
In this tutorial, we will be creating a VM and configuring Azure Sentinel to display global attack data (RDP Brute Force) on a world map in which we can actively monitor these attacks LIVE. <br />

<!-- <h2>Video Demonstration</h2>

- ### -->

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Firewall
- PowerShell
- Azure Sentinel (SIEM)
- 3rd Party API

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)

<h2>High-Level Steps</h2>

- Creating a Honeypot (Microsoft Azure's Vulnerable Virtual Machines/Computer)
- Disabling External and Windows Firewall
- Using Custom PowerShell scripts
- Creating a log repository for our exposed VM
- Setting up a Sentinel (SIEM)
- Using Sentinel (SIEM) to create a map that displays LIVE attacks
- Using 3rd Party API to derive geo-location (Lat, Long, State, Province, Country etc.) from PowerShell

<h2>Actions and Observations</h2>
</br>
</br>
<h3 align="center">
  Set up your virtual environment
</h3>
</br>
<p>
  First, let's create our Resource Group inside our Azure subscription and then create our Virtual Machine inside the Resource Group.
</p>
<p>
  <img src="https://i.imgur.com/ruA249D.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  While our VM is being created, we can go ahead and create our Log Analytics Workspace. Make sure the Resource Group aligns with the one you've created and make sure the regions match as well.
</p>
<p>
  <img src="https://i.imgur.com/RGINI6i.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  Next, lets go ahead to our Microsoft Defender for Cloud, go to Environment Settings, Enable all options, turn off SQL Servers and then click Save.
</p>
<p>
  <img src="https://i.imgur.com/DMMedkb.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
 Once saved - head over to Data Collection tab on the left and click "All Events".
</p>
<p>
  <img src="https://i.imgur.com/L1T04Ip.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  Now head back to your Log Analytics Workspace and connect your Honeypot VM.
</p>
<p>
  <img src="https://i.imgur.com/ptfuh3Z.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  It's going to take a few minutes to connecet to your VM - so lets go ahead and open a new Azure portal tab and create our Azure Sentinel.
</p>
<p>
  <img src="https://i.imgur.com/HG9v3IL.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  Once you opened to the Azure Sentinel page, click create and connect this to your Log Analytics Workspace.
</p>
<p>
  <img src="https://i.imgur.com/WrBMJvK.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  Now that everything is connected - head back to your Honeypot VM and let's connect to it with Remote Desktop. Remember to open the VM and copy the Public IP Address. MacOS users should download Remote Desktop.
</p>
<p>
  <img src="https://i.imgur.com/MDBRh6u.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  Using the provided Public IP Address - put the information into your Remote Desktop and remember to login with the information you put down when you created your virtual machine.
</p>
<p>
  <img src="https://i.imgur.com/urJnJVN.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  Sometimes you'll be asked to log in with your main computer, if that happens, just click more choices > other users and you'll be able to login with the username and password you created. 
</p>
<p>
  <img src="https://i.imgur.com/yvMeq6s.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  When you initially log into your VM, it may take a bit but that's normal. I personally uncheck all the initial requirements during bootup but it doesn't matter what you do. Once you're logged into the VM, head down to the search bar and type "Event Viewer" and open it up. It should look like this.
</p>
<p>
  <img src="https://i.imgur.com/OHDCrJB.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  Now on the left hand column, click on the "Windows Log" folder and you'll see a few dropdowns. Click the Security Tab. It should look like mine. It does take some time to load when you first open it, so be patient with it.
</p>
<p>
  <img src="https://i.imgur.com/DRz3DaU.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  Now when you initially look at the Event Viewer, you'll notice the left hand side of the chart will say Audit Successfull. We want to be able to see if we can see the Audit Failures and to do that, just go back to your main computer, open up ANOTHER Remote Desktop and intentionally input the wrong password 2-3 times. It should look like this in the Event Viewer tab once the logs see the attempted failed logins. We're primarily looking for Event ID 4625.
</p>
<p>
  <img src="https://i.imgur.com/cEIRUgG.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  When you open up an Event ID 4625, you'll see that the list provides you the workstation name and IP Address of the attempted log in. It doesn't show you the location though and I'm going to show you how to set that portion up as well using a 3rd party site.
</p>
<p>
  <img src="https://i.imgur.com/A5HKGwo.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
  Taking the IP Address that was given to us in the Event Viewer, we can use geolocation.io to take that IP Address and provide us the location of that IP Address by providing us the Latitude, Longitude, Country, City/Provinces etc.
</p>
<p>
  <img src="https://i.imgur.com/ZP1Os9N.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
    Before that, however, we need to make sure our VM is exposed for the world to discover. Let's go back to our main computer and open up your command prompt/powershell. Send a perpetual ping "Ping [IP Address] -t"; it should fail.
</p>
<p>
  <img src="https://i.imgur.com/ycyuFqO.jpg" height="75%" width="100%" alt=""/>
</p>
<p>
    
</p>
<p>
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
    
</p>
<p>
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
    
</p>
<p>
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
    
</p>
<p>
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
    
</p>
<p>
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
    
</p>
<p>
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
    
</p>
<p>
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
    
</p>
<p>
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
    
</p>
<p>
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
  
