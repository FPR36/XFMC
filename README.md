XFMC 3.72 – May 1 Update

The May 1 update for XFMC 3.72 is now available, bringing a substantial set of fixes, improvements, and new features. Below is the full changelog.
Fixes & Improvements

    Fixed double rudder mixing in the autopilot.

    Various internal arrays now reset correctly when XFMC is reset.

    Waypoint switching now works properly (previously fixed at 2 NM).

    XFMC now features a multicolor display.
    Note: personal color settings in XFMC.ini are no longer supported.

    In the leg list, the leg to steer is now highlighted in blue.

New Feature: Airspaces

    Airspace awareness has been added using the V‑cut method.
<img width="293" height="206" alt="afbeelding" src="https://github.com/user-attachments/assets/3c716a6c-8520-46a7-9e05-c4f4b00a3c3b" />

    Press the FIX key without entering a command to display surrounding airspaces.

    XFMC automatically selects airspaces relevant to the aircraft’s current altitude.

    Safe airspaces are shown as green lines.
<img width="288" height="227" alt="afbeelding" src="https://github.com/user-attachments/assets/d817728b-285c-447b-97f3-d85b403e89f5" />

    Airspaces the aircraft is currently inside are highlighted with an INSIDE label.
<img width="273" height="198" alt="afbeelding" src="https://github.com/user-attachments/assets/b6d4825b-6b68-4b2d-a090-bb6e3c6440e4" />


ACARS Page Enhancements

    The ACARS page now displays:

        METAR for departure and arrival airports.

        Arrival airspaces relevant to the flight.

    METAR data is retrieved from NOAA.

    If no METAR is available for the departure or arrival airport:

        XFMC searches the database for an airport with the same IATA code within 100 km.

        If none is found, no METAR is shown.

    Displayed METAR includes:
    ICAO code used + wind + temperature/humidity + QNH

Autopilot Logic Update

The built‑in XFMC autopilot has been refined for more realistic behavior:

    Pressing the AP button on the XFMC (light ON) now arms the autopilot, but does not engage it yet.

    The autopilot engages automatically once the aircraft climbs above the INITCLIMB altitude.

    Turning the AP button off fully disables the autopilot and returns control to manual.

    The autopilot remains active until the end of the ROLLOUT phase.

    Once the aircraft comes to a complete stop, the AP disengages automatically (light OFF).

    At any moment, the pilot can override the autopilot by switching AP to OFF.

    Takeoff autopilot activation now occurs in two steps:

        Pilot arms AP (light ON).

        AP engages automatically once above INITCLIMB altitude.

Database Update

    A new SQL database is included.
    Unpack the .rar into the root XFMC folder.
    =>The old SQL format (without airspace tables) is no longer supported.
    For a personal build:
    delete the SQL file from the root and start X‑Plane.
    A new database will be generated automatically (approx. 15 minutes).

XFMC‑CDU 1.20

    Airspaces are now displayed identically to the XFMC plugin.
    Added INSIDE airspace logic. 
    Zones will be filled with color (low alpha) when the plane enters a airspace zone.
    Every minute all drawn polygons will be repainted, removing older zones which are outside range
    Fixed a crash related to empty tiles, reported via Firebase.
    Likely caused by a race condition between internet loading and tile generation.
    Zones will be filled with color (low alpha) when the plane enters a airspace zone.
    Every minute all drawn polygons will be repainted, removing older zones which are outside range
=>Updated config files. Added Aerobask shark UltraLight plane. Read the note before using this plane!



XFMC 3.71—which includes the ability to generate the new SQL database—is planned for release as soon as it reaches the required stability level.

<img width="744" height="869" alt="afbeelding" src="https://github.com/user-attachments/assets/9c1b5a35-ca68-44d1-96a2-6dce937f4956" />
====================================================================================
XFMC 3.70 Release

XFMC 3.70 is now available.
This update does not introduce new features, and no bugs have been reported, but it includes a major internal restructuring of how navigation data is handled.
Background

Since its first release in 2009, XFMC has relied on multiple mixed data sources for navigation, airports, and ILS information:

    X‑Plane Apt.dat

    Navigraph airport and ILS data

    Navigraph SID/STAR, airways, and fixes, with fallback to X‑Plane fixes

Over time, discrepancies between these sources caused inconsistencies in airport detection, runway identification, and ILS alignment.
Examples of Data Mismatches

1. Small airstrips without ICAO codes  
X‑Plane can find local airstrips such as LF3624 – Levroux Grange Dieux, but XFMC could not, because it relied on the internal X‑Plane API.
In Apt.dat, these strips use an internal code like XLF006 on line 1, while the local identifier (e.g., LF3624) appears on line 1302.
XFMC could only find them if the internal code (e.g., XLF006Z) was entered manually.
Scanning Apt.dat directly solves this, but it is slow.

2. Airports with mismatched internal codes  
Example: FQCB  
XFMC and X‑Plane can both find the airport by ICAO, but XFMC could not detect its runways because Apt.dat uses an internal code like XFQ0002.

3. Navigraph vs. X‑Plane runway naming differences  
Some airports have runway sets like 21 / 21R / 21L in X‑Plane, but Navigraph may label them as 21L / 21C / 21R.
Selecting runway 21L in XFMC could therefore lead to the wrong physical runway heading.
The Solution: A Unified Internal SQL Database

XFMC now uses its own internal SQLite database, generated once from:

    X‑Plane Apt.dat

    X‑Plane earth_nav.dat

XFMC now uses Navigraph only for:

    Airways

    SID/STAR

    Fixes (with fallback to X‑Plane fixes)

This eliminates the inconsistencies between mixed data sources.
Database Generation

    Building XFMC.sql takes about 10 minutes, depending on CPU speed.

    The generated database is already included on GitHub.

    Custom scenery is scanned as well, and missing airports are automatically added to the SQL database.

XFMC‑CDU 1.17

    The prebuilt XFMC.sql is included in the release.

    For custom builds, the SQL file can be uploaded from an SD card or folder into the XFMC‑CDU internal storage.


-------------------------------------------------------------------
🚀 XFMC 3.6 – What’s New?
🛫 Improved fallback to X‑Plane airport data

When a departure or arrival airport was missing in Navigraph, XFMC didn’t always fall back correctly to the internal X‑Plane APT data.
This behavior has now been fixed — XFMC automatically selects the correct data source.
📡 Enhanced glideslope calculation

The GS needle now remains properly centered.
The underlying calculation has been reworked for a more stable and accurate approach.
🌬️ Wind compensation added to LOC

The localizer logic now compensates for crosswind.
Even with a 39‑knot sidewind, the aircraft stays aligned with the centerline.
🧭 More flexible LAT/LON waypoint input

You can now enter coordinates in multiple digital formats, including:

    0101N3499E

    01.01N34.99E  
    Both formats are now valid.

Waypoints entered without a decimal point are automatically interpreted as short‑format (xxyy).
📍 Improved “along track” waypoint function

The format XXXXXyyy/zz is now fully supported:

    XXXXX = waypoint

    yyy = course

    zz = distance in NM (max 40 NM)

Example:
SPL/180/25 creates a waypoint 25 NM south of VOR SPL.
Enter it in the console and click in the leg list where you want the waypoint inserted.
🛬 Fixed: KDFW 18R/18L arrival issue

The problems affecting the 18R/18L arrival procedures at KDFW have been resolved.
🖥️ XFMC‑CDU 1.14 – Improvements
🌍 Meridian crossing trackline fix

Tracklines crossing the meridian were sometimes displayed incorrectly.
This has now been corrected for accurate CDU rendering.
🔌 Crash fix for empty port number

If the port number field was left empty, the CDU could crash.
The port number is now validated before being stored.
🎉 A solid, stable release

XFMC 3.6 and XFMC‑CDU 1.14 deliver a mature, stable, and feature‑rich experience.
With these improvements, flight planning, navigation, and overall usability feel more precise and dependable than ever.===============================================================================
XFMC Release 3.56 – February 2026

Added

    Improved waypoint interception logic by monitoring distance and comparing previous results.

    Reinserted TOD/TOC waypoints into the leg list. This feature existed in early XFMC versions, was removed later, and is now added again to give the operator more information about the ongoing flight.<img width="502" height="783" alt="afbeelding" src="https://github.com/user-attachments/assets/e51bd8c9-c3a7-4392-8f7e-758bf3849161" />


    When a speed constraint is set in the descent phase, it will now be copied into the following waypoints.

    Added a configuration line for manual joystick blend from 50–100%. A value of 100% equals maximum sensitivity.

Info:  
In dedicated AP mode, X‑Plane joystick settings should be linear with no deadzone programmed. XFMC inserts the AP into the joystick channel. Manual joystick override has its own programmed deadzone and exponential response on each channel.

Fixed

    Corrected a bug in the fuel calculation. For small aircraft, reserve fuel is multiplied by 1000 (as in Boeing systems).

    Fixed an issue where a DISCON appeared at the arrival airport.

    Fixed issues with flight plans containing fixed waypoints with seconds (long numbers such as 4.414224434).

    The last entry in the leg list (arrival airport) is no longer skipped, preventing undesired heading commands in the final miles before arrival in non‑ILS mode.

    Fixed another issue in the leg list related to altitude and descent.

    Filtered a noisy dataref that caused pitch “kickups” in the XFMC pitch PID controller.

    Fixed a bug that reset reserve fuel to 0 when InitClimb was active.

Corrected

    Preflight must be completed before the AP can be switched on. Required items: V1, V2, Vref, fuel, runway, reserve fuel.

    For small aircraft, only 0.1 can currently be used as reserve fuel input (calculated as 100 lbs), or 0.0 if no reserve is desired.

    All preflight settings must be completed before the AP can be activated. “Preflight completed” will be shown on the takeoff screen when all conditions are met.

XFMC‑CDU

    Adjustments made for proper app closing and termination of the UDP channel.

    Fixes to avoid crashes caused by missing airport information from the simulator or corrupted data streams.

    Added a colortemplate selector for waypoints,plane etc.  4 basic templates are available

    Fixed a bug with a location pointer referenced in other functions, which caused strange track lines after waypoint manipulations.

Status
XFMC is close to its final state. It has come a long way from the early 2.7 version for X‑Plane 10 to the upgraded 3.56 for X‑Plane 12, with more than 1000 hours of test flights completed.

 
  Updated  Aircraftfiles XFMC + AP

Airliners

    LevelUp 737

    Zibo 737

    Standaard 737‑800

    X‑Crafts E175

    X‑Crafts E195

Business jets

    X‑Hanger Gulfstream 550

    Aerobask Phenom 300

General aviation / Light aircraft

    Aerobask DA42

    Aerobask DA62

Other

    Cirrus SF50 Vision Jet
===============================================================================


XFMC Update – January 2026
Version 3.55

The January 2026 update brings a series of refinements, bug fixes, and performance improvements aimed at delivering a smoother and more reliable XFMC experience. This release focuses heavily on navigation accuracy, approach stability, and overall system responsiveness.
Changes & Improvements

    Zibo DH logic corrected  
    The Decision Height handling for Zibo aircraft has been fixed for more accurate approach behavior.

    XFMC CDU timer updated to 2 seconds  
    Improves responsiveness while reducing unnecessary refresh load.

    Maximum flight level increased to FL450  
    Expanded altitude capability for high‑performance operations.

    Additional altitude tuning in the LEGS list  
    Further refinement of altitude handling for more consistent vertical planning.

    Fixed runway LLZ code issue around heading 360  
    Corrected a bug affecting localizer code detection on runways near 360°.

    Glideslope behavior improved  
    A margin has been added between the geometric glideslope and the ILS cone center to prevent premature descent during arrivals.

    GOA CCW/CD selection enhanced  
    When selected, GOA CCW/CD now displays [SEL]. Selecting again removes the GOA points as expected.

    ILS variable reset fix  
    Resolved an issue where switching to another runway during approach could leave the ILS variable in an incorrect state.

    Improved flap speed calculations  
    More accurate flap speed logic for both takeoff and approach phases.

XFMC CDU Update – Version 1.09

    Tracklist storage optimized  
    Tracklist duration has been adjusted to 20 seconds to prevent excessive growth and reduce memory usage
    Uploaded configs for Xcraft E175 and E195!  Video:  https://youtu.be/FNI7bX0PLEM
    ======================================================================================================================================================================
    
    New Year’s Update – Version 3.54

This update resolves several routing and navigation issues and introduces improvements to glideslope handling, navaid selection, and visual rendering within the XFMC CDU.
Route & Altitude Restriction Fixes

A number of bugs were identified in routes containing manually inserted fixes with altitude constraints. All have now been corrected:

    Simple routes such as
    ESSB .. ARTIB[7000] (manual fix) .. EHAM  
    previously produced an incorrect TOC. Fixed.

    Complex routes such as
    ESSB PETE1Z PETEV N872 ELPAX Z703 UMIXA KULUD EKDIV AMRAK EEL ARTIP[7000] (manual fix) .. EHAM  
    displayed a premature descent indication, even though the aircraft continued level flight. Fixed.

    Routes like
    ESSB PETEV[10000] (manual fix) N872 ELPAX Z703 UMIXA KULUD EKDIV AMRAK EEL EHAM  
    could generate an incorrect TOD. Fixed.

All three issues were caused by manual fixes with altitude restrictions inserted before or after the main route.
Glideslope Logic Improvements

The glideslope algorithm has been refined:

    The system now uses both the GS needle and a geometric reference calculation.

    GS tracking accuracy is improved to within 30 feet.

    At 200 ft AGL, the geometric calculation is terminated and a fixed 500 ft/min descent rate is applied.

Navaid Selection Enhancements

Routes such as
EGNX … LFBE  
with a manual fix like NDB MH or waypoint CF27 inserted immediately after EGNX could incorrectly select a distant navaid when multiple candidates existed in the search area.

    A list of all matching navaids is now generated.

    The closest navaid is automatically selected.

    This resolves issues caused by dense navaid environments. Fixed.

UI & Functional Updates

    Selecting an ILS in the Radio Page now displays [SEL].

    Activating a Vector Approach now shows [ACT].
    Reselecting it removes the API points.

    XFMC CDU updated to version 1.08.

Airport & Navigation Rendering

    Runways and ILS cones are now drawn for both departure and arrival airports.

    Navigation points now use proper symbols:

        Triangles for waypoints

        NDB icons for NDBs

        VOR icons for VORs

    Each navaid is labeled (e.g., ARTIB, EEL).

Important Note

The app must download the Apt data file (~300 MB).
Download time depends on your network speed.

The FMC screen will show the download status.
Wait until you see “DB Saved” before closing the app.  
Do not interrupt the download process.
<img width="584" height="819" alt="Schermafbeelding 2025-12-26 165807" src="https://github.com/user-attachments/assets/c36ca5c6-5a45-4e00-9869-b2624b90ba69" />
<img width="589" height="697" alt="Schermafbeelding 2025-12-26 165936" src="https://github.com/user-attachments/assets/69694075-cf6b-4165-856a-b21c7859454a" />

video of arrival LFBE with Zibo 4k and xfmc in dedicated AP mode  https://www.youtube.com/watch?v=Gng2A48ITY0





December 17, 2025 
XFMC Update 3.53 – Release Notes

Changes and Fixes:

    Resolved an issue when selecting a new SID/STAR: old SID/STAR waypoints are now properly cleared.

    Fixed compatibility issue with the x737 by Benedikt Stratmann.

    A/THR (Auto Thrust) now functions correctly.

    Note: The x737 operates only with the dedicated XFMC autopilot.
=============================================================================

December 8, 2025 – Release 3.51

    Fixed the issue with incorrect altitudes displayed in the leg list. Altitudes are now shown correctly again.

    Added a DISCON function to the leg list:

        Any turn to a waypoint that does not lie ahead within a certain angle will be marked with [DISCON].

        The user should verify whether the indicated waypoint is logical.

        DISCON entries can appear in SID, STAR, flight plan, or transition procedures.
=======================================================================================================================================<BR>
✈️ December St. Nicholas Update – XFMC 3.5

We’re excited to share the latest improvements in XFMC 3.5. This update focuses on refining approach logic, smoother ILS handling, and better integration with MCP and DH inputs. Below are the highlights:
🔧 Update Highlights

    Go-Around Logic

        Go-around now also resets the APP flag.

        Base leg calculation depends on MTO weight – larger aircraft require a wider turn radius.

    Cruise & MCP

        Descent via MCP in cruise mode now correctly holds altitude.

    ILS Approach Enhancements

        Extended to Intercept (ICEPT), Localizer (LLZ), and Glideslope (GS).

        APP button now displays: [ACT], [ICEPT], [LLZ], or [GS].

        Intercept requires a reasonable approach angle. Approaching at 90° risks missing GS capture.

    ILS Modules

        GS module: smoother, soft touchdown.

        LLZ module: softer capture behavior.

    VNAV Descent Page

        Speed/transition input fixed. Now supports:

            speed/xxx

            transition altitude/yyyyy

            or both xxx/yyyyy.

    Decision Height (DH)

        Previously only tied to X-Plane systems.

        Now also used by XFMC to enter the flare phase.

        Accepts DH inputs between 150–300 ft.

📊 Infogram – Descent & Approach Workflow
Descent

    Start Descent: set MCP to 0.

    Early Descent (<60NM): click DESCENT NOW.

    ATC descent to FLxxx: type xxx in command line → click MCP.

    ATC heading xxx:

        First disable LNAV.

        Then type HEADING/xxx in command line → click FIX.

Approach

    Select runway in use.

    Set ILS frequency by clicking on the ILS freq already shown by XFMC in the RADIO PAGE.

    Ensure altitude is 2000–3000 AGL and aligned to intercept.

    Click APP button in Approach screen.

APP Button States

    ACT → not in capture or intercept.

    ICEPT → aircraft not aligned to cone.

    LLZ → captured on horizontal beam.

    GS → glideslope captured.

Final Actions

    Deploy flaps and gear.

    As soon as the plane touches down, apply reverse thrust and brakes → aircraft transitions to rollout.
==================================================================================
✈️ XFMC Update – November

Version 3.4 (Desktop) Version 1.07 (Android App)
📱 XFMC App

    🔄 Sliders are now correctly restored when returning from sleep mode (Activity_Resume).

🔌 XFMC Plugin

    🐞 Bugfix: hidden issue fixed in climb restrictions below a level (B) and at waypoints far ahead.

    📈 Vertical Speed profile adjusted to better handle long-range v/s situations.

    🎛️ Dedicated Autopilot (AP) now includes Altitude Hold.

        MCP key refined to manage climb/descend during cruise phase.

    🛠️ Minor issues resolved.

🛫 Tested Aircraft

✅ Gulf550 (Xhangar) ✅ Phenom 300 (Aerobask) ✅ Standard 737 ✅ Zibo 737 ✅ x737 (Benedickt Stattmann)

📦 Configurations included in the attached ZIP
October 2025: Version 3.3 Released!

XFMC v3.3 introduces a fully integrated, dedicated Autopilot (AP) module — eliminating the long-standing compatibility issues with the native X-Plane autopilot.
XFMC now functions as a combined FMC + AP system, providing consistent and precise flight-path control across all supported aircraft.

✈️ Key Improvements

Integrated XFMC Autopilot:
The new internal AP handles LNAV, VNAV, ILS, and flare logic independently from X-Plane’s native systems, ensuring smooth and predictable behavior even on aircraft with custom logic (e.g. x737).

Configurable PID Tuning:
Each aircraft can now define its own PID control parameters in the configuration files, allowing fine-tuning of roll, pitch, yaw, and approach handling for specific flight models.

Enhanced ILS and Flare Handling:
Improved stability during final approach and touchdown, with logic refined for realistic flare altitude and pitch control.

XFMC App v1.06:
A new page has been added to the companion app, enabling real-time PID adjustments while in flight. Perfect for tuning responsiveness without restarting the sim.

⚙️ Notes

Existing configuration files will be automatically updated to include the new PID entries.

The dedicated AP operates with a 20 ms internal update rate for precise control feedback.

Backward-compatible with earlier XFMC flight plans and navigation data.
 XFMC Plugin – Version 3.3
Fixed: Vector approach now correctly handles Left/Center/Right runway arrivals.

Fixed: QNH mismatch issue where Flight Level on IVAO differed from Littlenavmap/X-Plane.

Added: Dedicated autopilot with ILS approach support.

Joystick can override steering.

XFMC generates a new config file with AP settings automatically.

PID parameters can be adjusted live via the Android AP interface (sliders).

Heading, VNAV, and altitude overrides are available on the panel.

To activate the dedicated AP, set dedicated AP = 1 in the config file.

To enable ILS approach:

Set the ILS frequency on the radio page.

Use the APP button on the approach page.

When on glideslope, APP [ACT] or APP [LOC] will appear.

Flare altitude and pitch angle can be configured.

Config files for various aircraft with dedicated AP will be provided later.

🔄 Update to version 3.3 using the provided updater 

===================================================================================================
XFMC for X-Plane 12 – A Relaunch<br/>
Background<br/>
Between 2011 and 2019, XFMC was available for X-Plane 9 and 10. Development was discontinued after the release of X-Plane 11. Recently, after purchasing X-Plane 12 and finding the default FMCs somewhat limited, I decided to revive XFMC and make it fully compatible with the latest version of the simulator.<br/>
Key Improvements<br/>
The entire codebase has been rewritten and updated. Major changes include:<br/>
•	Fixes for longstanding bugs<br/>
•	Proper handling of SID and STAR restrictions<br/>
•	Approach vector plots aligned with the runway<br/>
•	Full go-around support (both clockwise and counterclockwise)<br/>
•	Added Decision Inhibit functionality<br/>
•	Completely redesigned VNAV (Vertical Navigation)<br/>
•	Network support: connect an Android tablet to use XFMC as a remote CDU (Control Display Unit) and MAP<br/>
•	  <img width="200" height="300" alt="Screen Shot 08-19-25 at 12 44 PM" src="https://github.com/user-attachments/assets/de9fcbc1-3e39-4aba-a14f-64caf6430a11" />
<img width="200" height="300" alt="Screen Shot 08-19-25 at 12 43 PM" src="https://github.com/user-attachments/assets/e04dc5dd-fb34-4e1e-9599-42c84a8f2d6f" />

Supported Aircraft<br/>
XFMC is compatible with a wide range of aircraft, including:<br/>
•	All G1000-equipped aircraft (e.g. Cirrus SF50, Cirrus SR22, Aerobask Phenom, Aerobask DA62, Aerobask RB401, Laminar LanceAir, PiperAeroJet)<br/>
•	Default Laminar aircraft (B738, A333, MD82, Cessna X)<br/>
•	Zibo 4K<br/>
•	X737 by Benedikt Stratmann<br/>
Navigation Data<br/>
XFMC uses the Navigraph database, which provides SID/STAR and airport data. Without Navigraph, XFMC will fall back to X-Plane’s internal database (note: this does not include SID/STAR). To disable Navigraph support, open XFMC.ini and set: <br/>
EXTNAVPRIORITY=0<br/>
Package Contents<br/>
•	Full documentation<br/>
•	Quick setup guide for Android tablets<br/>
•	Configuration files for different aircraft<br/>
•	Installer/Updater tool<br/>
Installation Guide<br/>
1.	Unzip the installer to a dedicated folder.<br/>
2.	Run the installer and point it to your X-Plane 12 directory. Click Save.<br/>
3.	<br/>  
4.	Restart the installer if necessary and select Install XFMC.<br/>
5.	Wait until the message files unpacked appears (installation time depends on internet speed).
Updating<br/>
•	Launch the installer.<br/>
•	The server release version (e.g. 3.26) and your local XFMC.ini version will be displayed.<br/>
•	If they do not match, an Update button will appear.<br/>
•	Click it to download the latest win.xpl and place it in /plugins/XFMC/64/.<br/><img width="200" height="100" alt="Screen Shot 08-21-25 at 01 35 PM" src="https://github.com/user-attachments/assets/1231d1cc-29a6-4449-bf56-eb1364ed4245" />

Platform Support<br/>
•	Supported: Windows, Android tablets<br/>
•	Not supported: iOS, Linux<br/>
Configuration Notes<br/>
XFMC ships with preconfigured aircraft settings, including automation of flaps, gear, <br/>transponder, and other systems. If you prefer manual control, open the aircraft’s .ini file and set:<br/> 
CONFIG=0<br/>
Each aircraft .ini file must be placed in the same folder as the aircraft’s .acf file. For <br/>example, for the B738:    X-Plane 12/Aircraft/Laminar/B738/b738.ini<br/>
Final Notes<br/>
This is a personal, non-commercial project and will remain freeware. If you encounter bugs, please report them only if they can be reproduced consistently.<br/>
Happy flying!<br/>
✈️ Quick Setup Guide: XFMC & ATC/CTR (dedicated AP use)
🛫 Flight Preparation
📄 Load flight plan (SimBrief → XFMC import).

🛤 Select departure runway/SID.

📊 Enter cruise level in Performance page.

🛬 (Optional) Select arrival STAR.

➡️ If no ILS arrival:

Go to Approach page → click VECTORS.

XFMC builds vector approach with API, REF, THRSH points.

⚙️ Pre-Takeoff Setup
🎛 Set MCP altitude dial in aircraft.

Or type FL in command line → click MCP.

📝 On Takeoff page:

Select flaps.

Click V1, V2, REF.

🚕 Taxi to runway hold → click AP button in XFMC.

📡 If CONFIG bit 7 (128) set → transponder auto ON.

🚀 Takeoff
🛣 Line up on centerline → full throttle.

🔔 Wait for “PULL UP” prompt.

🎮 Pull joystick gently → hold until INIT-CLIMB.

✋ Release gradually → maintain positive climb.

🛫 XFMC takes over climb → respects restrictions → levels at FL.

☕ Relax, time for coffee!

📡 ATC Instructions (Enroute)
🧭 Heading change:

Disable LNAV → set heading bug.

Hack: type HEADING/XXX → click FIX.

📍 Waypoint change:

Type waypoint in command line → click first line of LEGS page.

If shortcut: deletes points between duplicate waypoints.

If far ahead: remove intermediate points to avoid illogical routing.

✈️ Cruise
🛑 Plane levels at programmed FL.

⬆️ To climb: enter new FL → click MCP.

⬇️ To descend (CTR instruction): same procedure.

🛬 Arrival & Descent
📐 Check VNAV Page 3 → TOD.

🎛 Before TOD: set MCP altitude in aircraft (not XFMC MCP).

⬇️ Early descent (ATC):

Enter new FL → click MCP.

If within 60 nm of TOD → VNAV Page 3 → DESCEND NOW.

🧭 Heading/waypoint changes: same as cruise.

📡 ILS Arrival
📻 Select ILS frequency on Radio Page.

🛬 On Approach Page → click APP → becomes APP [ACT].

📏 Ensure altitude 2000–3000 ft AGL before intercept.

🔒 When APP [LOC] shows → plane on glideslope.

Set flaps.

⚡ Adjust speed via VNAV Page 3, ECON speed, or manual throttle.

🛑 Cut engines ~200 ft AGL → flare at 20–30 ft AGL.

🛞 Apply brakes/RTO after touchdown.

🛬 Non-ILS Arrival
➡️ Use vector approach or program arrival plan.

⚡ Adjust approach speed in VNAV Page 3 (e.g., ECON 250 → ~200).

🧭 Vector approach aligns runway, but manual heading/speed may be needed.

✋ Flare pitch-up must be done manually (not automatic).
