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
  <img src="" height="75%" width="100%" alt=""/>
</p>
<p>
