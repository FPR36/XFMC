XFMC for X-Plane 12 – A Relaunch<br/>
Background< br / >
Between 2011 and 2019, XFMC was available for X-Plane 9 and 10. Development was discontinued after the release of X-Plane 11. Recently, after purchasing X-Plane 12 and finding the default FMCs somewhat limited, I decided to revive XFMC and make it fully compatible with the latest version of the simulator.< br / >
Key Improvements< br / >
The entire codebase has been rewritten and updated. Major changes include:< br / >
•	Fixes for longstanding bugs< br / >
•	Proper handling of SID and STAR restrictions< br / >
•	Approach vector plots aligned with the runway< br / >
•	Full go-around support (both clockwise and counterclockwise)< br / >
•	Added Decision Inhibit functionality< br / >
•	Completely redesigned VNAV (Vertical Navigation)< br / >
•	Network support: connect an Android tablet to use XFMC as a remote CDU (Control Display Unit) and MAP< br / >
•	  
Supported Aircraft< br / >
XFMC is compatible with a wide range of aircraft, including:< br / >
•	All G1000-equipped aircraft (e.g. Cirrus SF50, Cirrus SR22, Aerobask Phenom, Aerobask DA62, Aerobask RB401, Laminar LanceAir, PiperAeroJet)< br / >
•	Default Laminar aircraft (B738, A333, MD82, Cessna X)< br / >
•	Zibo 4K< br / >
•	X737 by Benedikt Stratmann< br / >
Navigation Data< br / >
XFMC uses the Navigraph database, which provides SID/STAR and airport data. Without Navigraph, XFMC will fall back to X-Plane’s internal database (note: this does not include SID/STAR). To disable Navigraph support, open XFMC.ini and set: < br / >
EXTNAVPRIORITY=0< br / >
Package Contents< br / >
•	Full documentation< br / >
•	Quick setup guide for Android tablets< br / >
•	Configuration files for different aircraft< br / >
•	Installer/Updater tool< br / >
Installation Guide< br / >
1.	Unzip the installer to a dedicated folder.< br / >
2.	Run the installer and point it to your X-Plane 12 directory. Click Save.< br / >
3.	< br / >  
4.	Restart the installer if necessary and select Install XFMC.< br / >
5.	Wait until the message files unpacked appears (installation time depends on internet speed).
Updating< br / >
•	Launch the installer.< br / >
•	The server release version (e.g. 3.26) and your local XFMC.ini version will be displayed.< br / >
•	If they do not match, an Update button will appear.< br / >
•	Click it to download the latest win.xpl and place it in /plugins/XFMC/64/.< br / >
Platform Support< br / >
•	Supported: Windows, Android tablets< br / >
•	Not supported: iOS, Linux< br / >
Configuration Notes< br / >
XFMC ships with preconfigured aircraft settings, including automation of flaps, gear, < br / >transponder, and other systems. If you prefer manual control, open the aircraft’s .ini file and set:< br / > 
CONFIG=0< br / >
Each aircraft .ini file must be placed in the same folder as the aircraft’s .acf file. For < br / >example, for the B738:    X-Plane 12/Aircraft/Laminar/B738/b738.ini< br / >
Final Notes< br / >
This is a personal, non-commercial project and will remain freeware. If you encounter bugs, please report them only if they can be reproduced consistently.< br / >
Happy flying!< br / >
