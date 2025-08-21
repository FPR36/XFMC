XFMC for X-Plane 12 – A Relaunch
Background
Between 2011 and 2019, XFMC was available for X-Plane 9 and 10. Development was discontinued after the release of X-Plane 11. Recently, after purchasing X-Plane 12 and finding the default FMCs somewhat limited, I decided to revive XFMC and make it fully compatible with the latest version of the simulator.
Key Improvements
The entire codebase has been rewritten and updated. Major changes include:
•	Fixes for longstanding bugs
•	Proper handling of SID and STAR restrictions
•	Approach vector plots aligned with the runway
•	Full go-around support (both clockwise and counterclockwise)
•	Added Decision Inhibit functionality
•	Completely redesigned VNAV (Vertical Navigation)
•	Network support: connect an Android tablet to use XFMC as a remote CDU (Control Display Unit) and MAP
•	  
Supported Aircraft
XFMC is compatible with a wide range of aircraft, including:
•	All G1000-equipped aircraft (e.g. Cirrus SF50, Cirrus SR22, Aerobask Phenom, Aerobask DA62, Aerobask RB401, Laminar LanceAir, PiperAeroJet)
•	Default Laminar aircraft (B738, A333, MD82, Cessna X)
•	Zibo 4K
•	X737 by Benedikt Stratmann
Navigation Data
XFMC uses the Navigraph database, which provides SID/STAR and airport data. Without Navigraph, XFMC will fall back to X-Plane’s internal database (note: this does not include SID/STAR). To disable Navigraph support, open XFMC.ini and set: 
EXTNAVPRIORITY=0
Package Contents
•	Full documentation
•	Quick setup guide for Android tablets
•	Configuration files for different aircraft
•	Installer/Updater tool
Installation Guide
1.	Unzip the installer to a dedicated folder.
2.	Run the installer and point it to your X-Plane 12 directory. Click Save.
3.	  
4.	Restart the installer if necessary and select Install XFMC.
5.	Wait until the message files unpacked appears (installation time depends on internet speed).
Updating
•	Launch the installer.
•	The server release version (e.g. 3.26) and your local XFMC.ini version will be displayed.
•	If they do not match, an Update button will appear.
•	Click it to download the latest win.xpl and place it in /plugins/XFMC/64/.
Platform Support
•	Supported: Windows, Android tablets
•	Not supported: iOS, Linux
Configuration Notes
XFMC ships with preconfigured aircraft settings, including automation of flaps, gear, transponder, and other systems. If you prefer manual control, open the aircraft’s .ini file and set: 
CONFIG=0
Each aircraft .ini file must be placed in the same folder as the aircraft’s .acf file. For example, for the B738:    X-Plane 12/Aircraft/Laminar/B738/b738.ini
Final Notes
This is a personal, non-commercial project and will remain freeware. If you encounter bugs, please report them only if they can be reproduced consistently.
Happy flying!
