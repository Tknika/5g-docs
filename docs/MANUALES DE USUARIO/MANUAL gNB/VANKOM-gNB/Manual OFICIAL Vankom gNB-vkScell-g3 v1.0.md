![][image1]

vkScell-g3 5G Pico gNodeB Manual 

All rights reserved 

Vankom Technology Co., Ltd. 

This material and all contents contained therein are the property of Vankom  Technology Co., Ltd. (Vankom) and are protected by the laws of the People's Republic  of China and applicable international conventions on copyright. Without the written  authorization of Vankom Technology Co., Ltd., no one shall copy, disseminate,  distribute, modify or otherwise use part or all of the contents of this material in  any form, and violators will be held liable according to law. 

Template Number: Version: V1.0.0 implemented on September 3, 2020

I   
![][image2]

Table of Contents 

1 Introduction ............................................................................................................................................ 1 

![][image3]Introduction ..................................................................................................................................1 ![][image4]Explanation of terms.....................................................................................................................1 ![][image5]Readers..........................................................................................................................................1 2 Product Introduction............................................................................................................................... 1 

![][image6]Introduction to the device.............................................................................................................1 2.1.1 API description ................................................................................................................1 2.1.2 Introduction to the indicator...........................................................................................2 

![][image7]Key skill indicators.........................................................................................................................3 3 Instructions for base station operation................................................................................................... 4 

![][image8]Base station provisioning process.................................................................................................4 3.1.1 Parametric planning ........................................................................................................4 3.1.2 Hardware connection checks..........................................................................................4 3.1.3 The device is powered on................................................................................................5 3.1.4 Base station parameter configuration.............................................................................5 3.1.5 Device restart..................................................................................................................9 3.1.6 Cell status inquiry..........................................................................................................10   
![][image9]Commonly used function configurations....................................................................................10 3.2.1 Maximum transmit power modified .............................................................................10 3.2.2 Software version upgrades............................................................................................11 3.2.3 Neighbors are added.....................................................................................................11 4 Instructions for using the LMT interface ............................................................................................... 18 

![][image10]LMT landing page........................................................................................................................18 ![][image11]system .........................................................................................................................................18 4.2.1 The menu bar collapses/expands with the current page position................................18 4.2.2 Customize the device name ..........................................................................................19 4.2.3 The operating status of the device................................................................................19 4.2.4 SSH..................................................................................................................................20 4.2.5 Restart your device........................................................................................................20 4.2.6 Download the how-to ...................................................................................................21 4.2.7 Change your password..................................................................................................21 4.2.8 Restart LMT ...................................................................................................................22 4.2.9 Sign out .........................................................................................................................22 ![][image12]Overview .....................................................................................................................................23 4.3.1 Device resource usage...................................................................................................23 4.3.2 The operating status of the device................................................................................24 4.3.3 Board temperature........................................................................................................24 4.3.4 GPS information .............................................................................................................24 4.3.5 Alarm information.........................................................................................................25 4.3.6 Base station information...............................................................................................25 4.3.7 The running status of the PLF/RAN/OAM service ..........................................................26 4.3.8 Base station capabilities................................................................................................26

I   
![][image13]

4.3.9 Community information................................................................................................26 ![][image14]Real-time information.................................................................................................................27 4.4.1 Operational status.........................................................................................................27 ![][image15]Rapid provisioning.......................................................................................................................28 4.5.1 Quick start.....................................................................................................................28 4.5.2 Quick search..................................................................................................................31 4.5.3 Common configurations................................................................................................32 Configuration management........................................................................................................32 4.6.1 Basic configuration........................................................................................................32 4.6.2 Security configuration ...................................................................................................34 4.6.3 QOS.................................................................................................................................35 4.6.4 base station...................................................................................................................36 4.6.5 Parameter comparison..................................................................................................39 Software management................................................................................................................40 4.7.1 Base station upgrades...................................................................................................40 4.7.2 Version switching ..........................................................................................................42 Community management ...........................................................................................................42 4.8.1 Community information................................................................................................42 4.8.2 Community initiation process.......................................................................................43 4.8.3 Cell configuration ..........................................................................................................44 Neighborhood management.......................................................................................................44 4.9.1 Neighborhood information ...........................................................................................44 4.9.2 Neighborhood configuration.........................................................................................44 Alarm management ..................................................................................................................45 Performance management .......................................................................................................46 4.11.1 counter........................................................................................................................46 4.11.2 KPI.................................................................................................................................47 4.11.3 Real-time counting ......................................................................................................47 Log management.......................................................................................................................48 4.12.1 Base station logs..........................................................................................................48 4.12.2 System logs..................................................................................................................49 System administration...............................................................................................................49 4.13.1 Scheduled tasks...........................................................................................................49 4.13.2 Parameter Authorization (Administrator) ...................................................................50 4.13.3 Role Authorization (Administrator).............................................................................50 4.13.4 User Management (Administrator).............................................................................51 4.13.5 System configuration...................................................................................................51

I 

1 preface 

Introduction 

This manual describes the equipment appearance, functional  characteristics, configuration, and maintenance operation methods of the  base station. The common problems that may be encountered are also explained  in the annotations, providing technical guidance for operators to correctly use, install,  open and maintain the equipment.  

Explanation of terms 

table 1Explanation of terms 

| name  | interpretation  | remark |
| ----- | ----: | ----- |
| LMT  | Maintain the terminal locally |  |
| OAM  | Operation and maintenance management |  |
| WITH  | Centralized unit |  |
| Of the  | Distribution units |  |
| PHY  | Physical layer |  |
| PLF  | platform |  |
| 5GC  | Core network |  |
| PLMN  | Public Land Mobile Network |  |
| TAC  | Track region codes |  |
| Slice\_SST  | Slice type |  |
| Slice\_SD  | 切片差分器（Slice Differentiato） |  |

Readers 

This book is suitable for: 

⚫ Engineering and technical personnel 

⚫ Open the commissioning personnel 

⚫ Operation and maintenance personnel 

⚫ Version testers 

2 Product Introduction 

Introduction to the device 

2.1.1 API description 

Figure 1 shows the interface diagram of the 5G integrated base station

**1** / **55** 

fig 1Base station interface diagram   
Table 2 describes the interfaces of 5G integrated base stations. 

table 2Base station interface description 

| seri  al   numb  er  | interface  | Description of the interface and its functions  |
| ----- | ----- | ----- |
| 1 | ANT1/2/3/4 | The external antenna interface corresponds to 4 antennas respectively,  and the configuration of 2 antennas can only be connected to 1 and 4  ports. |
| 2  | PWR-12VDC  | Power interface, 4 DC 12V power inputs |
| 3 | GE | Gigabit electrical port, which can be used as a return port or LMT  interface |
| 4  | SFP1  | 10GE optical port, backhaul interface, connected to the core network |
| 5  | SFP2  | 10GE optical port, reserved for expansion |
| 6  | USB  | Support USB2.0  |
| 7  | TST |  / |

//GE 端口默认 IP 172.20.50.1 

2.1.2 Introduction to the indicator 

  fig 2Schematic diagram of the indicator light   
Table 3 describes the base station interfaces. 

table 3Description of the base station indicator

| Silk screen  name  | type  | color  | state  | illustrate  | use  |
| :---: | ----- | ----- | ----- | ----- | ----- |
| POWER | power   supply | green | extinguish  | There is no power input  | Power status  indication |
|  |  |  | The green  | There is a power input  |  |

**2** / **55** 

|  | Light  |  | light is   always on |  |  |
| ----- | ----- | ----- | ----- | ----- | ----- |
| RUN/ALM | The status  of the   entire   machine  Light | Green/Red Bicolor | The green   light is   solid or   flashing | Solid on: The cell is   running normally,   flashing: Slow flashing in  cell activation: Out in  cell configuration: The  cell is abnormal |  |
|  |  |  | Flash red   fast or   slowly | High-level alerts flash  fast  Low-level alarms flash  slowly | Indication   of the   operating   status of   the system |
| ACT/LINK1 | Fiber link  status   indicator | green | extinguish | The internal link was not  successfully established  | SPF0 link   status   indication |
|  |  |  | The green   light is   always on | The internal link is   established normally |  |
| ACT/LINK2 | Fiber link  status   indicator | green | extinguish | The internal link was not  successfully established  | SPF1 link   status   indication |
|  |  |  | The green   light is   always on | The internal link is   established normally |  |

Key skill indicators 

The main skill indicators of the integrated base station are as follows: table 4Base station specifications

| serial  number  | The name of the  metric  | Metric values  |
| ----- | ----- | ----- |
| 1  | Frequency bands  are supported  | 5G N41/N78  |
| 2 | Carrier fan  capacity | One 100MHz 4T4R cell or two 100MHz 2T2R cells are supported |
| 3 | The number of  users in the cell | Each cell supports no less than 64 active users and no less than  200 RRC connected users.  |
| 4 | Channel bandwidth  is supported | IBW 100MHz, carrier bandwidth supports 20MHz, 40MHz, 50MHz, 60MHz,  80MHz, 100MHz |
| 5 | Maximum transmit  power | 4 channels, 250mW per channel  |
| 6 | Device   synchronization  mode | IEEE1588v2 clock synchronization is supported |

**3** / **55** 

| 7  | size  | 306mm\*234mm\*67mm (length \* width \* height). |
| :---- | :---- | :---- |
| 8  | weight  | 3.6kg |
| 9  | Power supply mode  | Quad DC 12V Supply, Voltage Range ± 10% |
| 10  | antenna  | External antennas |
| 11 | Operating   temperature | Long-term working temperature: \-40°C\~+50°C |
| 12 | Operating relative  humidity | 10％～95％ |

3 Instructions for use of base station operation All changes to the parameters in this section must be restarted to take  effect.   
Base station provisioning process 

3.1.1 Parametric planning 

Table 4 lists the parameters required for base station activation. table 5Parameter planning table 

| Parametric planning  |  |
| ----- | ----- |
| The name of the  parameter | illustrate |
| IP address of the  base station   service | eGTPU-IP 地址、NGAP-IP 地址,与核心网 N2/N3 可进行 ping 通。 |
| Frequency of work  | Frequency of community work |
| Working bandwidth  | Cell operating bandwidth |
| Frame structure  | Cell working frame structure |
| Antenna mode  | 2T2R/4T4R/2T2R-KS（天线复制模式） |
| PLMN  | Consistent with the core network |
| PCI  | Physical cell identification |
| TAC  | Cell tracking area code |
| NG interface IP  | IP address of the core network AMF |

3.1.2 Hardware connection checks 

As shown in Figure 3, check the wiring of the device before powering  on to ensure that the line connection is correct, as follows: a) Check the power connection to  

ensure that the power cord is properly connected to the DC 12V  power module and that the connection is tightened and not loose. 

**4** / **55** 

b) Check the connection of the antenna port  

to ensure that the RF port of the base station is connected to the  antenna and ensure that the connection is not loose.  

c) Check the 1588 to  

make sure that the optical port is connected to a clock server and  that the clock signal can be synchronized.  

d) Optical port inspection 

Make sure that optical port 1 is connected to the core network or  is on the same switch as the core network, and the optical module  rate is 10 Gbit/s. 

3.1.3 The device is powered on 

When the hardware connection check is completed, the device can be  powered on (DC12V), and the base station can be started after 3 minutes of  power-on, and the power indicator is always on.   
3.1.4 Base station parameter configuration 

3.1.4.1 login 

Connect the computer to the GE interface of the base station, enter  the 172.20.50.1 (default) address in the browser to enter the LMT login  page; You can also log in by connecting the computer to the optical port  and entering the optical port address 

On the login page, you can click \[Verification Code\] to switch, fill  in the correct user name, password, and verification code, and click \[Login\]  to enter the LMT system, as shown in the figure. 

Account: admin 

Password: lmt\_2023

**5** / **55** 

3.1.4.2 Modify the IP address of the base station 

After logging in to LMT, click \[Configuration Management\] \-- \[Basic  Configuration\] \-- change the eth0 address to Chapter 3.1.1 to plan the IP  address of the base station business, if you need to add multiple IPs,  click \[addresses\] \-- click \[+\] to add, and then click \[Save\]. 

3.1.4.3 Frequency/frame structure/channel number configuration 

After logging in to LMT, click \[Quick Configuration\] \-- \[Quick Station  Opening\] \-- click \[cell 333\] \--- select the frequency, frame structure and   
**6** / **55** 

number of antennas \-- and then click \[Open Station\]. 

The following table describes the number of antennas: 

2T2R：1、4 port TX and RX 

4T4R：1、2、3、4 port TX and RX 

2T2R-KS: 1 or 2 channels to 3 or 4 channels (antenna connection 1, 2  or 2 or 4\) 

3.1.4.4 Clock modifications 

After logging in to LMT, click \[Quick Configuration\] \-- \[Quick Station  Opening\] \-- click \[Base Station Parameters\] \-- configure \[Clock Source  Configuration\] to 0 \-- and then click \[Open Station\].  

 Parameter description: 

0：1588  

1: GNSS (not supported by this device) 

2:Freerun 

3.1.4.5 NG transport configuration 

After logging in to LMT, click \[Quick Configuration\] \-- \[Quick Site  Opening\] \-- Click \[Base Station Parameters\] \-- CU\_eGTPU-IP Address,  CU\_NGAP-IP Address, CU\_XNAP-IP Address, and AMF Server Address to the 

**7** / **55** 

address planned in Chapter 3.1.1 \-- and then click \[Open Site\]. If the N2 and N3 addresses of the core network are different, follow  this step.CU\_eGTPU 

Click \[Quick Configuration\] \-- \[Quick Search\] \-- fill in  IPInterfaceIPAddress in the search box, then click the Enter key, modify  the IP according to the response shown below, and then click \[Save and  Deliver\].   
3.1.4.6 PLMN configuration 

After logging in to LMT, click \[Quick Opening\] \-- \[Operator ID\] \-- Modify PLMN that is consistent with the core network \-- Click \[Open Site\]. **8** / **55** 

3.1.4.7 TAC configuration 

After logging in to LMT, click \[Quick Opening\] \-- \[Important Parameters  of the Community\] \-- \[Basic Configuration\] \-- Modify the code of the 5GS  tracking area to be consistent with the core network \-- click \[Open Site\]. 

3.1.4.8 Slice configuration 

After logging in to LMT, click \[Quick Opening\] \-- \[Network Slicing\] \- \- Modify the Slice\_SST and Slice\_SD to be consistent with the core network  \-- click \[Open Site\]. 

3.1.5 Device restart 

After the parameters are configured, restart the device for the  

parameters to take effect. 

After logging in to LMT, click \[Overview\] \-- click \[Restart Device\] \- \- click \[OK\].

**9** / **55** 

3.1.6 Cell status inquiry   
After logging in to LMT, click \[Overview\] \-- \[Community Information\]  to view the running status of the community, and if it is activated, the  community will be established successfully.  

Commonly used function configurations 

3.2.1 Maximum transmit power modified 

After logging in to LMT, click \[Quick Configuration\] \-- \[Common  Configuration\] \-- enter the power to be modified in the power value (the  unit is dbm, and it will be automatically calculated as W after input) \-- and then click \[Save\].

**10** / **55** 

3.2.2 Software version upgrades 

After logging in to LMT, click \[Software Management\] \-- \[Base Station  Upgrade\] \-- Click \[Upload File\] to upload the upgrade package \-- click \[OK\]  \-- if the cell is in a fault state before the upgrade, the rollback policy  should be turned off \-- click \[Upgrade\]. 

Rollback policy: If the detection cell is not activated after the  

upgrade, the version will be rolled back. 

During the restart phase of the upgrade process, you need to wait for  the restart to complete the automatic connection on the current page, or  you can manually refresh it later. 

3.2.3 Neighbors are added 

Measurement Event Interpretation: 

A1: The service cell is better than a certain threshold, and the  measurement is turned off, and the unit is dBm 

A2: If the service cell is below a certain threshold, open the  measurement, in dbm 

A3: The adjacent cell is better than the current service cell by a 

**11** / **55** 

certain value, which is mostly used for co-frequency switching, and the  unit is db 

A4: The adjacent cell is better than a certain threshold, and it is  mostly used for different frequency switching, in dbm 

A5: The service cell is lower than a certain threshold, and the adjacent  cell is better than a certain threshold, which is mostly used for frequency  switching, unit dBm 

B1: The adjacent area of the different system is better than a certain  threshold, and it is mostly used for the switching of different systems,  in dbm 

B2: The service cell is lower than a certain threshold value, and the  adjacent cell of the different system is better than a certain threshold  value, which is mostly used for different frequency switching, unit dBm 3.2.3.1 Measure switch configuration 

1\> Turn on the A1/A2 measurement switch:  

After logging in to LMT, click \[Configuration Management\] \-- \[Base  Station\] \-- \[CU\] \-- \[Power Control Information\] \-- \[Default Measurement  Parameter Configuration during UE Initial Access\] \-- Change \[A1  Measurement Switch\] and \[A2 Measurement Switch Configuration\] to 1 \-- 

click \[Save and Issue\].  

2\> Turn on the A3 measurement switch of the same frequency:  

Simultaneous frequency switching changes this configuration; After logging in to LMT, click \[Configuration Management\] \-- \[Base  Station\] \-- \[CU\] \-- \[Power Control Information\] \-- \[Default Measurement   
**12** / **55** 

Parameter Configuration during UE Initial Access\] \-- Change \[Same  

Frequency A3 Measurement Switch\] to 1 \-- Click \[Save and Issue\].  3\> Turn on the A4 measurement switch:  

Change this configuration if the frequency is switched; 

After logging in to LMT, click \[Configuration Management\] \-- \[Base  Station\] \-- \[CU\] \-- \[Power Control Information\] \-- \[Measurement  Parameter Configuration after A2 Measurement Received\] \-- Change  \[Frequency A4 Measurement Switch\] to 1 \-- Click \[Save and Issue\].    
3.2.3.2 Measurement configuration 

1\> Measurement Configuration:  

The default can be used for co-frequency measurement; 

The cross-frequency measurement configuration is as follows: After logging in to LMT, click \[Neighborhood Management\] \-- \[Neighborhood Management\] \--\[Linkage Area Configuration\]-- \[MeasControlLsit\]--\[MeasContro\[name=meas1\]\]-- 

\[InterFreq\[InterFreq\[MeasContro\[name=meas1\]\]--\[InterFreq\[InterFreq--

**13** / **55** 

Click \[+\] \- fill in the ssb frequency, subcarrier spacing, and BAND of  the adjacent cell \- click \[OK\]. 

(Multiple transience measurements can be added) 

2\> Measurement Event Thresholds:  

Log in to LMT and click \[Neighborhood Management\] \-- \[Neighborhood  Configuration\]--\[MeasControlLsit\]--\[MeasContro\[name=meas1\]\]-- \[EventConfig\]--\[A1Event\]--点击\[TriggerQuantityThreshold\]-- Configure  the corresponding event type according to the event type enabled in  conjunction with the measurement switch, and set the corresponding  value for \[ThresholdRSRP\].  

ThresholdRSRP Parameter definition: 156 minus this parameter is the  

absolute value dbm

**14** / **55** 

Example: 

A1 Event Configuration: 

If ThresholdRSRP is set to 81, the corresponding threshold value is  156-81=75 dBm.  

3.2.3.3 Add neighbors 

3\> To add a co-frequency neighbor:  

a) Log in to LMT and click \[Neighborhood Management\] \-- \[Neighborhood  Configuration\]--\[NeighborList\]--\[IntraFreqCell\]--Click \[+\] \-- Fill  in the neighboring area PLMN,CID,SCS,PCI,TAC — Click OK.  
**15** / **55** 

b) Configure BAND 

Click on the neighbors that have been added—click\[NRTDDInfo\]-- \[NRFreqBandList\]--\[NRFreqBandItem\]-- Modify the band value \- Click  \[Save & Deliver\].   
c) Configure the SSB frequency 

Click on the added neighborhood—click \[MTC\]--\[MeasTimingItem\]-- modify the ssb frequency—click \[Save and Deliver\].   
d) Multiple PLMNs can be added to the same frequency neighborhood Click on the added neighborhood—click \[+\] \- fill in PLMN \- click \[OK\]. 

**16** / **55** 

4\> To add a frequency neighbor:  

a) Log in to LMT and click \[Neighborhood Management\] \-- \[Neighborhood  Configuration\]--\[NeighborList\]--\[InterFreqCell\]--点击\[+\]-- Fill in  the neighboring cell’s PLMN, CID, SSB frequency number,SCS,  PCI,TAC,BAND — Click OK.  
**17** / **55** 

4 Instructions for using the LMT interface 

In the operation instructions, the login user is the administrator  permission, and the system can support the current mainstream browsers  including Chrome 85 or above (recommended), Edge85 or above, and Firefox  79 or above.   
LMT landing page 

Enter the correct management port (default 172.20.50.1) or optical port  address in the browser to enter the LMT login page. 

On the login page, you can click \[Verification Code\] to switch, fill  in the correct user name, password, and verification code, and click \[Login\]  to enter the LMT system, as shown in the figure. 

Account: admin 

Password: lmt\_2023 

system 

4.2.1 The menu bar collapses/expands with the current page  position 

The left side of the system is the operation menu, you can click the  button in the lower left corner \[Collapse/Expand\] menu bar; The upper right  corner is the title of the current main page, which is automatically updated  with page switching. As shown in Fig.

**18** / **55** 

4.2.2 Customize the device name 

The middle part is the current device name, you can click \[Name\] to  enter the editing mode (the maximum custom name is 20 characters), as shown  in the figure.   
4.2.3 The operating status of the device 

The right side of the device name displays the current running status  of the device, you can click Refresh, and it supports automatic refresh  configuration, configuration location: \[System Management/System  Configuration \-- Auto Refresh/Base Station Status\]

**19** / **55** 

4.2.4 SSH 

The upper right corner of the system is the global operation button,  

click \[SSH\] to enter the command line mode, as shown in the figure. 

4.2.5 Restart your device 

Click \[Restart device\] to automatically identify the current restart  type, click restart and wait on the current page, and the system can be  automatically connected after the restart is successful.

**20** / **55** 

4.2.6 Download the how-to 

Click \[Current User\] and drop down menu \[Operation Instructions\] to  download the current version of the operation instructions to the local  computer.   
4.2.7 Change your password 

Click \[Change Password\], you can enter the original password/new  password and click \[OK\] to change the password, and you need to log in  again after changing the password.

**21** / **55** 

4.2.8 Restart LMT 

Click Restart LMT and Confirm to restart LMT. 

4.2.9 Sign out 

Click Sign Out and Confirm to log out of the current user login status.

**22** / **55** 

Overview 

On the overview page, the device running status, alarm information,  base station information, 5GC running status, UPF running status, PLF  running status, RAN running status, OAM running status, base station  capability, and cell information are displayed as follows.   
4.3.1 Device resource usage 

Display and update the CPU, memory (hover over \[Memory Usage\] to display  the total memory, used memory, and available memory), disk usage, and  change trend in real time, as shown in the figure, click \[View Details\] to  jump to the real-time information details page, and display the CPU usage  

by core (please refer to the 2.4 Real-time Information section).**23** / **55** 

4.3.2 The operating status of the device 

The device information, startup time, and running duration are  

displayed, as shown in the figure. 

4.3.3 Board temperature 

Display and update the board temperature and trend in real time, as  

shown in the figure. 

4.3.4 GPS information 

Display GPS information, including: latitude and longitude, altitude,  signal strength, as shown in the figure.

**24** / **55** 

4.3.5 Alarm information 

To display the statistics of the four levels of alarms that are  currently active, click Refresh Information to manually refresh the  statistics (see 2.13 System Management/System Configuration for automatic  refresh configuration), and click View Details to jump to the alarm  information details page (see 2.10 Alarm Management), as shown in the  figure.   
4.3.6 Base station information 

Displays the basic information of the current base station, including  the serial number, hardware version, software version, and clock source  information, as shown in the figure.

**25** / **55** 

4.3.7 The running status of the PLF/RAN/OAM service Display the PLF/RAN/OAM running status, startup time, and running  duration, click the Refresh Status button to refresh the current running  status, and click the Start/Stop button to start and stop the corresponding  service, as shown in the figure. 

4.3.8 Base station capabilities 

The specific capabilities of the current base station are displayed,  

as shown in the figure. 

4.3.9 Community information 

Displays all cells of the current device, and supports manual refresh 

**26** / **55** 

of the cell running status, as shown in the figure. 

Real-time information 

4.4.1 Operational status 

Display and update base station information in real time: RRC access  success rate, number of UEs, antenna RSSI, board temperature, support for  custom update frequency, configuration location \[system management/system  configuration \-- automatic refresh/real-time information/base station  information\]; 

Display and update device information in real time: CPU core usage,  memory usage, update frequency 1s; 

As shown in Fig.

**27** / **55** 

Rapid provisioning 

4.5.1 Quick start 

4.5.1.1 Parameter modification/site opening 

After the corresponding parameter device value column is modified,  click \[Changed Parameters\] to view the current modified parameters, click  the \[Delete\] button to delete the modifications, restore the parameter  values, and after all the modified parameters are verified, click \[Open  

Station\] and \[Confirm\] to save and distribute, as shown in the figure.

**28** / **55** 

4.5.1.2 Modify associated parameters 

After the main parameters of the associated parameters are modified,  other parameters in the same group are automatically synchronized to the  modified state, and the non-primary parameters can be modified separately  

again, as shown in the figure. 

4.5.1.3 Export the template 

Click Export Template to export all the parameters of the current fast  website as a template .xlsx format file, as shown in the figure.

**29** / **55** 

4.5.1.4 Import parameters 

After modifying the required device values in the export template,  click \[Import Parameters\], select the file and click \[OK\] to perform the  correct parameter import, the imported parameters will automatically match  the modified values and update them on the page, and then click \[Open Site\]  

to send them after checking that they are correct. 

4.5.1.5 Site opening guidance 

Menu: \[Quick Configuration/Quick Station Opening\] 

You can quickly switch/configure the main parameters through the  navigation items, including: base station basic information, network  management information, and each cell parameter, as shown in the figure.

**30** / **55** 

4.5.2 Quick search 

Menu: \[Quick Configuration/Quick Search\] 

4.5.2.1 Parametric search 

Support parameter name fuzzy search, can be automatically prompted  according to the input character, \[Enter\] or click the \[Search\] button to  perform the search, the results will highlight the keyword (up to 64 search  results are displayed, more results need to be re-searched with precise  search conditions), as shown in the figure. 

4.5.2.2 Modify & Save 

The modification and saving of search parameters are the same as those  in 2.5.1.   
4.5.2.3 Parameter positioning 

Click Parameter Name to automatically jump to the specific  configuration structure of the parameter under configuration management,  as shown in the figure.

**31** / **55** 

4.5.3 Common configurations 

It supports modifying the power value of the cell, \[Enter\] or clicking  \[Save\] (the save button will automatically appear after the power value is  modified) to send it, as shown in the figure. 

Configuration management   
4.6.1 Basic configuration 

4.6.1.1 Network configuration 

Menu: \[Configuration Management/Basic Configuration\] 

Display the current network configuration, hover over each node, and  display the operation items supported by the node; 

Click the node to modify it, and click the icon on the right to perform 

**32** / **55** 

related operations, as shown in the figure. 

4.6.1.2 Time zone configuration 

Menu: \[Configuration Management/Basic Configuration\] 

The time zone can be modified, as shown in the figure.

**33** / **55** 

4.6.2 Security configuration 

4.6.2.1 Generic configuration 

Menu: \[System Administration/Security Configuration\] 

Support to display the status, display and modify the pre-shared key,  ConfigDeploy, and switches, and click \[Confirm\] to modify the switch after  

toggling the \[Switch\] state, as shown in the figure. 

Click \[Configuration\] to modify the pre-shared key/ConfigDeploy, and  

click \[Save and Deliver\] to perform the delivery operation, as shown in  

the figure. 

4.6.2.2 Channel configuration 

Displays all channel configuration information, supports adding and  deleting channels, and modifies channel parameters, as shown in the figure.

**34** / **55** 

4.6.3 QOS 

MENU: \[CONFIGURATION MANAGEMENT/QOS\] 

4.6.3.1 Key messages 

THE MAIN QOS INFORMATION OF EACH CELL IS DISPLAYED IN THE FORM OF A  LIST OF CELLS, AS SHOWN IN THE FIGURE.   
4.6.3.2 QOS CONFIGURATION 

CLICK THE \[QOS CONFIGURATION\] BUTTON ON THE "MAIN INFORMATION"  INTERFACE TO SWITCH TO THE QOS DETAILED PARAMETER CONFIGURATION INTERFACE,  CLICK THE \[ADD\] BUTTON ABOVE THE CONFIGURATION STRUCTURE TREE TO PERFORM  ADD, AND CLICK THE \[DELETE\] BUTTON ON THE RIGHT SIDE OF THE QOS NODE OF 

**35** / **55** 

THE CONFIGURATION STRUCTURE TREE TO DELETE IT, AND THE MODIFICATION  OPERATION IS THE SAME AS 2.5.1 QUICK OPENING OF THE SITE, AS SHOWN IN THE  

FIGURE. 

4.6.4 base station 

4.6.4.1 Profiles 

Menu: \[Configuration Management/Base Station/Configuration File\] Displays all configuration files of the current base station. Upload file: Click Upload File, select the configuration file and click  OK to perform the upload, as shown in the figure. 

➢ Export File: Click \[Export File\] to export the current configuration of the device, as shown in the   
**36** / **55** 

figure; 

➢ Add a note: Click the \[Edit\] button in the comment column to customize the note information for  

the specified profile, and click \[OK\] to submit, as shown in the figure; 

➢ Import configuration file: Click the \[Import\] button to import the specified configuration for the  

device, as shown in the figure, you **need to wait for the service to restart after the prompt message  is completed before proceeding with other operations**;  

➢ Download the configuration file: Click the \[Download\] button to download the specified  configuration file to the local computer, as shown in the figure. 

➢ Delete a profile: Click the \[Delete\] button to delete the specified profile, as shown in the figure.

**37** / **55** 

4.6.4.2 OAM 

Menu: \[Configuration Management/Base Station/OAM\] 

Parameter information can be displayed by category, and the parameters  of CU, DU, PHY, PLF, and OAMCFG can be saved and delivered in a unified  manner (the modification and delivery operations are the same as those in  2.5.1 Quick Start), and the main view of the classification and the main  view of the parameter list can be switched, as shown in the figure.   
Click Parameter Name to view the parameter definition information, as shown in the figure.

**38** / **55** 

4.6.4.3 WITH 

菜单：\[配置管理/基站/CU\] 

The operation is the same as OAM. 

4.6.4.4 Of the 

Menu: \[Configuration Management/Base Station/DU\] 

The operation is the same as OAM. 

4.6.4.5 PLF 

Menu: \[Configuration Management/Base Station/PLF\] 

The operation is the same as OAM. 

4.6.4.6 OAMCFG 

Menu: \[Configuration Management/Base Station/OAMCFG\] 

The operation is the same as OAM. 

4.6.5 Parameter comparison 

Menu: \[Configuration Management/Parameter Comparison\] 

To display the list of uploaded profiles, you can edit  notes/download/delete, click the \[Compare\] button to compare the parameter  differences between the selected profiles and the current device, wait for  the comparison to be completed, and display the list of differences by  parameter category (filter by category is supported), as shown in the  figure.

**39** / **55** 

Software management 

4.7.1 Base station upgrades 

Menu: \[Software Management/Base Station Upgrade\] 

Displays the current software version and all upgrade file information,  and supports modifying the rollback policy and uploading the upgrade file,  as shown in the figure.

**40** / **55** 

Click \[Upgrade\] and \[Confirm\] to execute the upgrade file, as shown in  the figure, and display the real-time upgrade progress when the upgrade is  executed. 

During the restart phase of the upgrade process, you need to wait for  the restart to complete the automatic connection on the current page, or  you can manually refresh it later. 

Specify the upgrade file, click \[Delete\] and \[Confirm\] to delete the  upgrade file, as shown in the figure.

**41** / **55** 

4.7.2 Version switching 

Menu: \[Software Management/Version Switching\] 

Displays the version information of all installed software of the  current base station, identifies the conflicting version and the current  version, and supports version switching, deletion, and information refresh,  as shown in the figure.   
Community management 

Menu: \[Community Management\] 

4.8.1 Community information 

Displays all the basic information of the community. 

➢ Create a community: Click \[Create Community\], enter the cell name, and click \[Confirm\] to create  

the community, as shown in the figure;

**42** / **55** 

➢ Update Template: Click \[Update Template\], select the template community and \[Confirm\] execution,  as shown in the figure; 

➢ Refresh the cell running status: Click the \[Refresh\] button to re-obtain the cell running status; ➢ Activation/deactivation: Click the \[Activate\]/\[Deactivate\] button of the designated cell to perform  the activation/deactivation operation; 

➢ Cell configuration: Click the \[Configuration\] button of the designated cell to jump to the cell  configuration page (see the next section on cell configuration); 

➢ Delete the cell: Click the \[Delete\] button and \[Confirm\] to delete the cell. 

4.8.2 Community initiation process 

Click on the cell list/current running status to view the cell startup  process, as shown in the figure.  
**43** / **55** 

4.8.3 Cell configuration 

Click the \[Configuration\] button of the specified community to jump to  the cell configuration page, you can modify the corresponding parameters,  and execute the save and delivery (the operation is the same as 2.5.1 to  quickly open the station), as shown in the figure. 

Neighborhood management   
Menu: \[Neighborhood Management\] 

4.9.1 Neighborhood information 

To display the 5G/4G neighborhood information under each cell, click  \[Neighborhood Configuration\] to jump to the neighborhood configuration page,  

as shown in the figure. 

4.9.2 Neighborhood configuration 

Display the parameters of the neighborhood, support modify/save the 

**44** / **55** 

delivery (the same as 2.5.1 quick site opening), and support add/delete,  where add is to add sub-parameters, and delete is to delete this level of  

parameters, as shown in the figure. 

You can select a template cell and update the template, as shown in  

the figure. 

Alarm management 

Menu: \[Alarm Management\] 

Displays the current active alarms, historical alarms, and event alarm  information, and the automatic update cycle can be configured (please refer  to 2.13 System Management/System Configuration for automatic refresh  configuration), supports manual refresh, and supports clicking \[Alarm  Number\] to view the alarm knowledge base, as shown in the figure.

**45** / **55** 

Performance management 

4.11.1 counter 

Menu: \[Performance Management/Counter\] 

All counter groups are displayed, you can select counter groups, view  the corresponding counter data by category, and export all/manually refresh,  as shown in the figure.

**46** / **55** 

4.11.2 KPI 

Menu: \[Performance Management/KPI\] 

View KPIs by category, support export all/manual refresh, as shown in  the figure. 

4.11.3 Real-time counting 

Menu: \[Performance Management/Real-Time Counting\] 

The count information is updated in real time, and the auto-refresh  frequency can be modified (for details about the auto-refresh configuration,  see 2.13 System Management/System Configuration), as shown in the figure.

**47** / **55** 

Log management 

4.12.1 Base station logs 

Menu: \[Log Management/Base Station Log\] 

Displays the base station logs of the current version and previous  versions. 

It contains logs such as CU and DU, and displays the total size of logs  in the current category, the folder where the current logs are located,  and the list of all logs. 

Support fuzzy search by name in the current display list; 支持修改 CU/DU/OAM/PHY 日志级别; 

Support deleting/batch deletion of log files (folders); 

Support online viewing/downloading of log files; 

As shown in Fig.

**48** / **55** 

4.12.2 System logs   
Menu: \[Log Management/System Log\] 

The system logs are displayed, and the logs of the operation are the  same as the base station, as shown in the figure. 

System administration 

4.13.1 Scheduled tasks 

Menu: \[System Administration/Scheduled Tasks\] 

Displays the scheduled task file of the current device, which can be  edited/diff/saved, as shown in the figure.

**49** / **55** 

4.13.2 Parameter Authorization (Administrator) Menu: \[System Management/Parameter Authorization\] 

As shown in the figure, you can edit the visible/writable status of  parameters in the Configuration Administrator role, check multiple boxes  to determine whether the parameters are visible, and configure whether the  

parameters are writable by using the writable switch. 

**Note: After the system is deployed, the administrator needs to authorize the parameters first,  and then the configuration administrator and the common user can perform normal operations.** 4.13.3 Role Authorization (Administrator) 

Menu: \[System Administration/Role Authorization\] 

All user roles and corresponding operation permissions are displayed,  and administrators can modify and configure administrator permissions, as 

**50** / **55** 

shown in the figure. 

4.13.4 User Management (Administrator) 

Menu: \[System Administration/User Management\] 

Displays all user information of the current system, supports  adding/deleting users (the current user cannot be deleted), and resetting  the password, as shown in the figure, in which you need to log in again  after resetting the current user password. 

4.13.5 System configuration 

Global configuration is supported: 

➢ Alarms, real-time information/base station information, real-time performance counting, cell  operation status, base station status (top row), service status (overview page) refresh frequency; ➢ Parameter list display column (whether to display the parameter path name/English name); ➢ The overview page displays the service items;   
As shown in Fig.

**51** / **55** 

**52** / **55**

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAC4AAAAuCAYAAABXuSs3AAAEYUlEQVR4XtWZW6gVVRjHv9NNsqASUbIepAu+SHmBKAgK7cEHixI3VErm3qdZa7SQgigiUMonX6KXoA7BwQep3dXjdmat2RuMBCOylxDPQwhW9nAipUw9Hc/F/uubc6lvzz5nZjt7n+YPPzbM7Fnff61Z37oNUbvavfsapteuIhW9SMq+F2O+Ji8cIhWMMV5wCdcHSZtPGD96i1TjKdr2xa1M11SpLiLPejBwjNHmIulwokeHV9Lg/otnxkjbnxnf9lE5WE2l6rUyVL4qlPG171/PKLMFwQZJhePSULtMVuQ8GuFDdJ3lTC7a+tkS9OEqo01uhpOA+V8YZTcjco+0kl5+cB9a+CRaeMIhA3UKNNAI+fU90286swpnfLu5n/HtKVlot4D5y+ie+5hUiVs5uJR0NBjTvVZOIh59gG9eIroyS58vVW+A4c/jTM9qOpjEIMnsBBhltB3v8W3C/9MD839hIntY2p1RYY2r8Pl2DMPgHxjGPo1pVMgbeIjKX66IObQSgTfi3tuMjk64199czuygAb5Dw97CTOuZgcWMtj/KB1qBCo4yfv1jPLeSEyhNEnkIrOtlVPYnRpvhlFwiL9LMTGHo/I6UMyJm0L9R0OuMl2W4+peeO3QH4w2sSc322l1MLLSSsscd0mASaGVkevQGxTPbLJnecRXVeG/wIMwMO6TJJDCmHuTRZ97l21fSDn9o6QvYOKyVRcyPlOmTBluB7lSnR45cJ4vIRc/WbqMd9Zf/g2qBbuwssHEdfisNtgLj9asyXm4qVW9GI/7ukHEl2MtOYAwPz8kbzRiGKrVNMl5+wsbbrx93NMdvxk3zc0+/vmHohdpjMlx+wupP2yOOpvgJFNi4F/4pL7aCvMNPynD5CV3FLaSAjJsEktN8Ly+2gsf8Tmnr/ptg+jeHjCuJk1OZfnmjFViWBqlWgO1oS3AnEvMAo6OPYmwyKuovsHE/ei31lK+wE6lg5/+/kAofhaERhzSaBLdEp2bPTOJ9pj3hkCaTwJu5HO+651uFNe7khW8yGGak0SSIT2jrPtNuspaqi5ht4fLUPH1gKTOtcrSM0faMNNkKcsdkjh22j7zgbp5AmDlUOnYjqcZmrP5OMr49l47oLNjFNMmLNxXS5Fyg6wyR3+hnvGgTVcw92NwujglvR+I/ML259u03+B2dOYdpLi8Jcsfb7uTY0aSNAwtR6FfyoSzEQ6txh0HDjLYj+B1LO+QmEZ8qRE9IuzMqrHEnFd2LQGccsoBuA8PjjK7vxepx7vzBhngd40dDsrBuQXxKa/czG4IF0uLs6j28Dq/616t5ze3gTtSwZvkAyb2QyazCGncqhyvQx47GdNY88amvo7Ern/XQVM3d0Zs2/AZk0KuB3GcTHVk0zmqmI0d77rRU2T1I3NOMW7tkrEjcFex5RtsaJr7HacO7GRMwqwprfEpTXwe8aD0q8g5MHGW0PQ1jF7BgG58EFTNuL/kD475auE/qblngSLO+SdA/YhGhwdEPQoEAAAAASUVORK5CYII=>

[image2]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAC4AAAAuCAYAAABXuSs3AAAEYUlEQVR4XtWZW6gVVRjHv9NNsqASUbIepAu+SHmBKAgK7cEHixI3VErm3qdZa7SQgigiUMonX6KXoA7BwQep3dXjdmat2RuMBCOylxDPQwhW9nAipUw9Hc/F/uubc6lvzz5nZjt7n+YPPzbM7Fnff61Z37oNUbvavfsapteuIhW9SMq+F2O+Ji8cIhWMMV5wCdcHSZtPGD96i1TjKdr2xa1M11SpLiLPejBwjNHmIulwokeHV9Lg/otnxkjbnxnf9lE5WE2l6rUyVL4qlPG171/PKLMFwQZJhePSULtMVuQ8GuFDdJ3lTC7a+tkS9OEqo01uhpOA+V8YZTcjco+0kl5+cB9a+CRaeMIhA3UKNNAI+fU90286swpnfLu5n/HtKVlot4D5y+ie+5hUiVs5uJR0NBjTvVZOIh59gG9eIroyS58vVW+A4c/jTM9qOpjEIMnsBBhltB3v8W3C/9MD839hIntY2p1RYY2r8Pl2DMPgHxjGPo1pVMgbeIjKX66IObQSgTfi3tuMjk64199czuygAb5Dw97CTOuZgcWMtj/KB1qBCo4yfv1jPLeSEyhNEnkIrOtlVPYnRpvhlFwiL9LMTGHo/I6UMyJm0L9R0OuMl2W4+peeO3QH4w2sSc322l1MLLSSsscd0mASaGVkevQGxTPbLJnecRXVeG/wIMwMO6TJJDCmHuTRZ97l21fSDn9o6QvYOKyVRcyPlOmTBluB7lSnR45cJ4vIRc/WbqMd9Zf/g2qBbuwssHEdfisNtgLj9asyXm4qVW9GI/7ukHEl2MtOYAwPz8kbzRiGKrVNMl5+wsbbrx93NMdvxk3zc0+/vmHohdpjMlx+wupP2yOOpvgJFNi4F/4pL7aCvMNPynD5CV3FLaSAjJsEktN8Ly+2gsf8Tmnr/ptg+jeHjCuJk1OZfnmjFViWBqlWgO1oS3AnEvMAo6OPYmwyKuovsHE/ei31lK+wE6lg5/+/kAofhaERhzSaBLdEp2bPTOJ9pj3hkCaTwJu5HO+651uFNe7khW8yGGak0SSIT2jrPtNuspaqi5ht4fLUPH1gKTOtcrSM0faMNNkKcsdkjh22j7zgbp5AmDlUOnYjqcZmrP5OMr49l47oLNjFNMmLNxXS5Fyg6wyR3+hnvGgTVcw92NwujglvR+I/ML259u03+B2dOYdpLi8Jcsfb7uTY0aSNAwtR6FfyoSzEQ6txh0HDjLYj+B1LO+QmEZ8qRE9IuzMqrHEnFd2LQGccsoBuA8PjjK7vxepx7vzBhngd40dDsrBuQXxKa/czG4IF0uLs6j28Dq/616t5ze3gTtSwZvkAyb2QyazCGncqhyvQx47GdNY88amvo7Ern/XQVM3d0Zs2/AZk0KuB3GcTHVk0zmqmI0d77rRU2T1I3NOMW7tkrEjcFex5RtsaJr7HacO7GRMwqwprfEpTXwe8aD0q8g5MHGW0PQ1jF7BgG58EFTNuL/kD475auE/qblngSLO+SdA/YhGhwdEPQoEAAAAASUVORK5CYII=>

[image3]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAAKCAYAAABSfLWiAAAAjklEQVR4XmNggAABKE4EYm6oGC7ABcQxQCwCxWCgB8RrofgFECvAJNCAEhQvA+IHQGwExWBAFUM0GSAaQfg4lMYG5JDwVgY0Q0CABYrxGYIMhrshokBsBcWXgTgAiGWgWBiIOxggFsDSkhkQHwXiWCgGxRhYsBmK24G4BYgdoBikqRSImYFYA4qR1YGwDwBdHx/x4WeL/wAAAABJRU5ErkJggg==>

[image4]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAALCAYAAACZIGYHAAAAvUlEQVR4Xq3SrQoCQRQF4Iv/ICIIBpvBrIKgYFrYoNFq0bJ2fx/Ax7CZNQkKvoEIFrvP4DN4rnPWHRZWWPTAV+6dOWVGxCRLfchxFk6aHBhCld4pw4ae9iIUj/awhRvpfemBS1eJLilSkg7U1eVfSjQpukh0iZ0EnKjpD+OWtOFMGX8Yp6QER2jRJ99KdK7J0w5GwTrIzyU1GNMDZtCgiph/oZ9sTXeYw5QckDosaAVL6FABJmJeY0B6xua+ABhgJfe0COSgAAAAAElFTkSuQmCC>

[image5]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAALCAYAAACZIGYHAAAAyUlEQVR4Xq3Rvw7BUBQG8KOIP4lRYjB0MTJJsBkkPICFibUxYLIaTAYrsXkKsQsGo9UjeAbf6f2uNE0qTfiSX5rck35p7xExyVAPsjwLJ01tGIJLfoqwpVdwEEqfdrCGO5V12IUO3SS6JE8JcOBELR3+pUSTootElwRTgyv5v6OJU1KgIzxgT59FxCmx0Q3pMg7k2cG3En1JkySbGW3swc8lVZjTE1bQoJKYO8jxXC1gAmdqglRgRGM+9faVrnQg5gtcmsIS6uS8Ad0CJ6jNR9DJAAAAAElFTkSuQmCC>

[image6]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAALCAYAAACZIGYHAAAAwklEQVR4XrXRMQtBYRQG4IMi5C/YrAxSYrlkMBoVG1IMFCalbEa7weYXWPwKgz9gNPkN3tN9T32+XBNvPct3zn2/270iIjEoQZ9qkJDoZKBNaTuswAX2dIWBDb0U4ARPyttAm5WlI2Fp3DmzdKEBN/ptiZ8eHP1DJzn5UpKlMwTvo7dEluir72gj4R+LyscSfWAEB3K/j5Yby/9KWvCALc1hDEmY0Jq7ZRjCnWZQ1UERVp4ppCS8QDV1EanDwtlbQvACcC4rqvg3hb0AAAAASUVORK5CYII=>

[image7]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAALCAYAAACZIGYHAAAA3UlEQVR4Xq3SPwuBURQG8ONPFCVlsFisBkpZlHqVwaIMsrAYZLBYTErZjLIalMHOplAGs6/hY3hO5xzdbq/NU7/lnnvPve+9LxFRBCowVHWIUXiy0IG+yluhBhfYqBeMregkClvYw1HdIcfFlLJ0SZryIj8ZkpNzjT2hyoW/NPEzgIM/6MWaPKDkFtLqBIFbCElP8b0kbJC7rtWS5Mi/wjvfVNEGeQG/xk6592PHtvspwBma6pu/NGnBG1ZqBhOSb+XmbAFxkle76hzTACrD3DOFJMkGrE3yF49C5gYfuZwn0U5HXn4AAAAASUVORK5CYII=>

[image8]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAALCAYAAACZIGYHAAAAyUlEQVR4XrXQuw4BQRgF4N8tIq6NVqVSUWxLaBQqobGFywPQKiUuD6BSKRR6HkOikHgGpXdwxpxJ/mx2O07yJTPz757sjohNDXzqQIrnYclAl8z6mwZcYEV3mLthIFU4w5sqbpAW1YiM4ar2OgNow5N+W+JSogMsAzOdvESUbOBGD/D0MJDIkiRkqS+2TP+iTmhJHGJug5TFfk0REorL/0p6sIcJneAotnxBWz7bFHvpL1rzTAowhB2NIGffkTq1uDcXPoUZmbX3AZETKvyrw7odAAAAAElFTkSuQmCC>

[image9]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAALCAYAAACZIGYHAAAA4klEQVR4Xq3SvQtBURgG8OM7H6GkbMwMMmCjlEkGJcUik81uYmBisVkkBrMMZGQjg/xFntd539vpxuap33DPc3rvOd2rlE4aOqwCHl63Jwp1aLGEFDnYw4g9YCClEQfMYQ1bdoUYlT7wW1v1aQ7Gs5mw0sOcjIYUqPjLEAndlyxhaBZfIkMukJHFMdzYC4pS/EiD7cAri24IMirvEJDSFnrziSVlkY5F95TE4QkRcBkoKThCiVn5y5AaLKDLNrBSenifzZT+Ac9KX3XKJlCFz2drGkUbQlQgWVZW+jS0r2eTfwPYsCckb09VYgAAAABJRU5ErkJggg==>

[image10]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAKCAYAAAC5Sw6hAAAAs0lEQVR4XrXRsQpBURzH8T8ihUwmpYyUsplkJaOSYrJJFoMXoLwCSRmVeAysPIHBg/ie7v/Wce7Z5Fuf4d5Tv7rninyXwAAt571bHmNkVKQ2Hti4B1Z1HPFGUUX6eSirTphjax86VVHCTTxDMzVFDzv70FNaPENlnFUOfewRV768Q0Nc1QV3vDBSvv47lJTgk0Jm+ICUMn9pgZgqoIknuspcT6SaBPcUVsHEem5giTVWqvMBgkYliLKmDwkAAAAASUVORK5CYII=>

[image11]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAALCAYAAAByF90EAAAA1UlEQVR4Xq3SPwuBURQG8Otf2ZQFo5JMmJQkGSSTpIhPgTL4FjZJGAwGZVAsSlnkM5h8FM95PVfXpTeDp37De+7b6d5zr1Lv8UAJ0lbdTBCq0IUofSQLd5hZdTMjWMMcrhTRi35awFi5NwqBlw6U14t/a5SjKbSUeyMdaXSijBRkJ0uSITfVb41k4BuSC1AV2JMMewBbiNG3xOECKXJSgxXJTRzhpp5HFPIkZNc6YdhBw6g5+VsjO/aMCjCBAMksz9CHHhVffxtJQt34TkAHfNSGoaX8AASvLKGkuEg8AAAAAElFTkSuQmCC>

[image12]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAALCAYAAAByF90EAAAA5ElEQVR4Xq3SPwtBURgG8NefJDtlUMqgTDIoDEoZDCal2E1SNsonMBgkg4UYZDMpgwwWvoCyWXwQz+O+N9ehO3nqV/ec0316u/eIfMYDRUgb+84EoQxNSKqvsOABG7FKyUwHpjCBq4rah341h7G4F4XkfXZSBfvwb0U5NYO6uBfZycBFxbjBSZYqBTVxL+JLe7iJ9Z2IU77+wE7loQ8HiKtfCUAEtqrFzQqs1QqOcIeG4lSc2o7P8TxQQy7+VmTG/Eb8IwuxLiKNoAttOKvs600jCSg51mGoyruYN7kn1iS8wOR9Ai/8L7X/xK5lAAAAAElFTkSuQmCC>

[image13]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAC4AAAAuCAYAAABXuSs3AAAEYUlEQVR4XtWZW6gVVRjHv9NNsqASUbIepAu+SHmBKAgK7cEHixI3VErm3qdZa7SQgigiUMonX6KXoA7BwQep3dXjdmat2RuMBCOylxDPQwhW9nAipUw9Hc/F/uubc6lvzz5nZjt7n+YPPzbM7Fnff61Z37oNUbvavfsapteuIhW9SMq+F2O+Ji8cIhWMMV5wCdcHSZtPGD96i1TjKdr2xa1M11SpLiLPejBwjNHmIulwokeHV9Lg/otnxkjbnxnf9lE5WE2l6rUyVL4qlPG171/PKLMFwQZJhePSULtMVuQ8GuFDdJ3lTC7a+tkS9OEqo01uhpOA+V8YZTcjco+0kl5+cB9a+CRaeMIhA3UKNNAI+fU90286swpnfLu5n/HtKVlot4D5y+ie+5hUiVs5uJR0NBjTvVZOIh59gG9eIroyS58vVW+A4c/jTM9qOpjEIMnsBBhltB3v8W3C/9MD839hIntY2p1RYY2r8Pl2DMPgHxjGPo1pVMgbeIjKX66IObQSgTfi3tuMjk64199czuygAb5Dw97CTOuZgcWMtj/KB1qBCo4yfv1jPLeSEyhNEnkIrOtlVPYnRpvhlFwiL9LMTGHo/I6UMyJm0L9R0OuMl2W4+peeO3QH4w2sSc322l1MLLSSsscd0mASaGVkevQGxTPbLJnecRXVeG/wIMwMO6TJJDCmHuTRZ97l21fSDn9o6QvYOKyVRcyPlOmTBluB7lSnR45cJ4vIRc/WbqMd9Zf/g2qBbuwssHEdfisNtgLj9asyXm4qVW9GI/7ukHEl2MtOYAwPz8kbzRiGKrVNMl5+wsbbrx93NMdvxk3zc0+/vmHohdpjMlx+wupP2yOOpvgJFNi4F/4pL7aCvMNPynD5CV3FLaSAjJsEktN8Ly+2gsf8Tmnr/ptg+jeHjCuJk1OZfnmjFViWBqlWgO1oS3AnEvMAo6OPYmwyKuovsHE/ei31lK+wE6lg5/+/kAofhaERhzSaBLdEp2bPTOJ9pj3hkCaTwJu5HO+651uFNe7khW8yGGak0SSIT2jrPtNuspaqi5ht4fLUPH1gKTOtcrSM0faMNNkKcsdkjh22j7zgbp5AmDlUOnYjqcZmrP5OMr49l47oLNjFNMmLNxXS5Fyg6wyR3+hnvGgTVcw92NwujglvR+I/ML259u03+B2dOYdpLi8Jcsfb7uTY0aSNAwtR6FfyoSzEQ6txh0HDjLYj+B1LO+QmEZ8qRE9IuzMqrHEnFd2LQGccsoBuA8PjjK7vxepx7vzBhngd40dDsrBuQXxKa/czG4IF0uLs6j28Dq/616t5ze3gTtSwZvkAyb2QyazCGncqhyvQx47GdNY88amvo7Ern/XQVM3d0Zs2/AZk0KuB3GcTHVk0zmqmI0d77rRU2T1I3NOMW7tkrEjcFex5RtsaJr7HacO7GRMwqwprfEpTXwe8aD0q8g5MHGW0PQ1jF7BgG58EFTNuL/kD475auE/qblngSLO+SdA/YhGhwdEPQoEAAAAASUVORK5CYII=>

[image14]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAKCAYAAAC5Sw6hAAAAx0lEQVR4Xq3SP8tBYRzG8R89HpMnZfEGrFYmfzIpRVmwIGVQkpLJLoMFg3fAJC9CBsuzKnkvvrf7d8R9ysJVn+Gcc3UN931EXhNCBynnvZsAGsgqX8q4YOp+cJIX21sqXz4eiqk9JvJ+KIwNBlioR8aqjp68H2pihIo4Qwls1R/6mCGovMTVDlFUsVL3XgsHZUr/OKOkvOTUSWzviKvqmkJLvjT0i8iTIeZi/ymjgDZ+lNerYa3MBfiSRvHpOSP2PNwkxR64ITeRfi+udwiJmwAAAABJRU5ErkJggg==>

[image15]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAKCAYAAAC5Sw6hAAAAzUlEQVR4Xq3SqwoCQRQG4MN6AcXLAwgWwWAw2A1iEYyCiHgpikEQg0EQLFaL2UsTg82sBl/AB/Bl/A/7L8wOspb94QszZ+YMs7Mi/kSgB3Vr3kwZxjSkrG8F0oA37O2CkSUcYAAdyvhWSAiNUnSBufxvNLInvSxoCi0JbqQH3eEMM0pooQBXSkMbjuCQHb1GDopwo4kWdOOD9JQXfKBPQVnTTgehNYpC0tCFE8RI/5sVxElfqyruCz+pJj9SgqYxzovb3PtmumkLG6iQ8wWd7ioyal3GuQAAAABJRU5ErkJggg==>