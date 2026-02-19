XFMC Release 3.56 – February 2016

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

======================================================================================================================================================================================
======================================================================================================================================================================================

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
