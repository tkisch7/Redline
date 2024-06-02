<h1>Redline</h1>

<h2>Description</h2>
In this lab we will be using Redline to conduct digital forensics. With redline you can take memory dumps and get a very good overview of what an endpoint looks like. This can be used to quickly assess the nature of a security event.

Here is a list of what you can do utilizing Redline:

- <b>Collect registry data</b>
- <b>Collect running processes</b>
- <b>Collect memory  images</b>
- <b>Collect browser history</b>
- <b>Look for suspicious strings</b>

There are three options to collect data using Redline:

- <b>Standard collector: this method configures the script to gather a minimum amount of data for the analysis, and only takes a few minutes to complete.</b>
- <b>Comprehensive collector: this method configures the script to gather the most data from your host for further analysis, this will take up to an hour or more to complete.</b>
- <b>IOC Search collector (windows only): This method collects data with the IOC that you created with the help of IOC editor.</b>
<br />


<h2>Languages and Utilities Used</h2>

- <b>Redline</b>
- <b>Mandiant IOC</b>

<h2>Environments Used </h2>

- <b>Windoqws Virtual Machine</b>

<h2>Lab Walk-through</h2>

<p align="center">
1. In this task we will use the standard collector method and choose the target platform. In our case, it would be windows. <br/>
<img src="https://imgur.com/dbO7vSk.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
<br />
<br />
2. In the Review script configuration, click on edit your script, this is a very important step since you can select what data needs to be collected. <br/>
<img src="https://imgur.com/y9KD7va.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
<br />
<br />
3. After configuring this we can go ahead and choose a folder to save our collected data to. You can choose any folder just make sure it is empty before.<br/>
<img src="https://imgur.com/uyMit1a.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
<br />
<br />
4. Once ‘okay’ is selected, a pop-up will appear and it will show steps you need to do to collect data from the host. A script named ‘RunRedlineAudit’ will appear. Run this script as Administrator to be able to collect all the data we need.<br/>
<img src="https://imgur.com/YCRkKyo.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
5. This will open up a Command prompt script once you run it. It might take up to 30 minutes to complete.<br/>
<img src="https://imgur.com/aRrOceW.png" height="80%" width="80%" alt="Splunk Searching Steps"/><br />
<br />
6. Once your analysis is done you will find it in the sessions folder. Since we have only run the script once it should be named AnalysisSession1. Run the .mans file and the data will be imported directly into redline.  <br/>
<img src="https://imgur.com/RGPJNJA.png" height="80%" width="80%" alt="Splunk Searching Steps"/><br />
<br />
7. First, we want to find out the OS of the system we just scanned. To find this we can click on the system information and look under the Operating System information table.<br/>
<img src="https://imgur.com/o0itvQs.png" height="80%" width="80%" alt="Splunk Searching Steps"/><br />
<br />
8. Next we will look at the scheduled tasks to see if anything is suspicious. Click on the Tasks on the left and analyze all the scheduled tasks. You should find something that sticks out and shouldn’t be there.  <br/>
<img src="https://imgur.com/6tCBcEC.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
9. There is a new System Event ID created by the intruder, search for events with the source name THM-Redline-User to find the event ID.<br/>
<img src="https://imgur.com/o0kbTUY.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
10. The intruder downloaded something onto the system, let’s look at our file downloads to see if there is anything out of the ordinary. After looking at the downloads you should find an app that sounds suspicious. You can see where it was downloaded and the website it was downloaded from. <br/>
<img src="https://imgur.com/katVoDg.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
11. For the next task we will look at the IOC editor. This should be located on your VM next to Redline on the task bar. IOC stands for Indicators of compromise; these are artifacts of potential compromises and intrusions on a host. We want to take some artifacts from a possible intrusion. We can load up our received artifacts into the system like this. <br/>
<img src="https://imgur.com/OOObWGB.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
12.	Next load up your saved IOC and run it in redline.<br/>
<img src="https://imgur.com/t9ttEYo.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
13. It will take a little bit of time to load up, once it is finished you will see the report pop up with ‘hits’. Here you can find out all the information about the file that matched up with the IOC file you created. <br/>
<img src="https://imgur.com/7IOOkdk.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
14. After listing out all the artifacts let’s analyze another endpoint. Click on the file on the desktop and run the .mans file. Let’s find out the product name/ OS. Like we did earlier, open the system information.  <br/>
<img src="https://imgur.com/amu9gBT.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
15. Next let’s look at the note that was left on the desktop for Charles. We can look by looking at the file system and analyze Charles’ desktop.  <br/>
<img src="https://imgur.com/mphHMvp.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
16. Now we want to see the Windows Defender service that ran, we can go to windows services to find that. Filter by Windows Defender and it should pop up. <br/>
<img src="https://imgur.com/VYwfJQv.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
17. The user manually downloaded a zip file, we can find this in the File Download History. Click on that and filter for zip files or manual downloads.<br/>
<img src="https://imgur.com/KeWe4jh.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
18. Now we need to look for the name of the executable that was dropped on the user’s desktop. To do this we can go back to the desktop and analyze the executables.  <br/>
<img src="https://imgur.com/tpTfSxM.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
 <br />
<br />
19. Take the file hash and search it on Virus Total. Here we can see that this is in fact a program called Cerber. <br/>
<img src="https://imgur.com/PUZF9A8.png" height="80%" width="80%" alt="Splunk Searching Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
