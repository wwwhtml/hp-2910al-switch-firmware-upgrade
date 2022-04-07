# HP Procurve 2910al Switch Firmware Upgrade, via SSH

This tutorial is based on a switch that was factory reset, that you have the firmware files ready in a local TFTP server, and that you have or know how to obtain the switch's IP Number. See important links at the end.

01. With an ethernet cable physical connect the switch to the local network, then turn the switch on.

02. From your computer connect the switch, for this tutorial the swith's IP is 192.168.0.184.
If the switch could handle newer encryption, the command could be simply like this: ssh 192.168.0.184, but because it doesn't we have to do it this way: 
<br><b>ssh -o KexAlgorithms=diffie-hellman-group1-sha1 -o Ciphers=aes256-cbc4 192.168.0.184</b>

03. Once connected, press ENTER.

04. Change to the configuration mode:
<b>config terminal</b>

05. To see what version do you have running: <b>show version</b>

06. To see what version is the primary and secondary firmware:<b>show flash</b>

07. To iniciate the download of the firmware from the TFTP server (for this tutorial the tftp server IP is 192.168.0.193, and firmware to upgrade is to w_15_14_0018.swi). example:<br>
<b>copy tftp flash 192.168.0.193 W_15_14_0018.swi</b>

08. Then press ENTER.

09. Press y to proceed: <b>y</b>

10. Press <b>1</b> to install it as the primary firmware.

11. Once downloaded, to see the file set to be the primary firmware run:<b>show flash</b>

12. Then to reboot for the firmware to be applied on the primary memory run:
<b>boot system flash primary</b>

13.Press ENTER.

14. Press: <b>y</b>

15. The install takes a minute or so to complete. 

-------------------------------------------------------------------------------------------------------

<b>How do I reset my HP Procurve 2910al to factory settings?</b>
"To execute the factory default reset on the switch, perform these steps:

Using pointed objects, simultaneously press both the Reset and Clear buttons on the front of the switch.
Continue to press the Clear button while releasing the Reset button.
When the Self Test LED begins to blink, release the Clear button." ~ 
https://www.raiseupwa.com/miscellaneous/how-do-i-reset-my-hp-procurve-2910al-to-factory-settings/#How_do_I_connect_my_Procurve_Switch

-------------------------------------------------------------------------------------------------------

<b>Firmware Download</b>: 
https://h10145.www1.hpe.com/downloads/SoftwareReleases.aspx?ProductNumber=J9146A&lang=&cc=&prodSeriesId=

-------------------------------------------------------------------------------------------------------

<b>Setting up SNTP</b>:
HP 2910al Switch SNTP Configuration<br> 
Using Apple's SNTP server's IP, time.apple.com = 17.253.82.253:<br>
<br>
<b>config terminal</b><br>
<b>sntp unicast</b><br>
<b>sntp 30</b><br>
<b>sntp server priority 1 17.253.82.253</b><br>
<b>timesync sntp</b><br>
<b>end</b><br>
<b>write memory</b><br>
<b>exit</b><br>
<b>show time</b><br>
<b>exit</b><br>
<b>exit</b><br>

========================================================================================================
