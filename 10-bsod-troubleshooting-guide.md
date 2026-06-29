1. CRITICAL_PROCESS_DIED
What the user experiences
The system suddenly crashes and restarts. Windows displays a blue screen indicating that a critical system process has stopped unexpectedly.
________________________________________
Step-by-step troubleshooting
Step 1: Boot into Safe Mode
Safe Mode loads Windows with minimal drivers, allowing diagnosis without interference.
How to do it:
1.	Restart PC
2.	Hold Shift + Restart
3.	Navigate to:
o	Troubleshoot → Advanced Options → Startup Settings
4.	Press F4 (Safe Mode)
📌 Image suggestion: Safe Mode menu screen
________________________________________
Step 2: Check system logs
Open Event Viewer:
eventvwr.msc
Go to:
•	Windows Logs → System
Look for:
•	Critical errors (red icons)
•	“CRITICAL_PROCESS_DIED”
📌 This identifies what service failed.
________________________________________
Step 3: Repair system files
Run Command Prompt as Administrator:
sfc /scannow
What this does:
•	Scans all protected system files
•	Replaces corrupted or missing Windows files automatically
Then run:
DISM /Online /Cleanup-Image /RestoreHealth
What this does:
•	Repairs Windows image itself (deeper repair than SFC)
•	Fixes corrupted update or system components
________________________________________
Outcome
System files repaired, system stability restored.
________________________________________
Learning
Most critical process failures are caused by:
•	Corrupted Windows updates
•	Failed system file updates
•	Malware interference
________________________________________
2. MEMORY_MANAGEMENT
What users experience
Random restarts or BSOD during heavy usage or startup.
________________________________________
Step-by-step troubleshooting
Step 1: Run Memory Diagnostic Tool
Press:
Windows Key + R
Type:
mdsched.exe
What happens:
•	System restarts
•	RAM is tested before Windows loads
•	Reports errors after reboot
📌 Image suggestion: Windows Memory Diagnostic screen
________________________________________
Step 2: Interpret results
After reboot:
•	Open Event Viewer
•	Navigate to:
Windows Logs → System
•	Look for MemoryDiagnostics-Results
________________________________________
Step 3: Hardware check
•	Power off PC
•	Remove RAM sticks
•	Re-seat RAM into slots
________________________________________
Outcome
Faulty RAM replaced or reseated → issue resolved.
________________________________________
Learning
•	RAM issues often mimic software crashes
•	Hardware validation is essential before software fixes
________________________________________
3. IRQL_NOT_LESS_OR_EQUAL
What users experience
Sudden BSOD when opening apps or connecting devices.
________________________________________
Step-by-step troubleshooting
Step 1: Enable Driver Verifier
Run Command Prompt as Admin:
verifier
Select:
•	Create standard settings
•	Select all drivers
What this does:
•	Forces Windows to check driver behavior
•	Identifies unstable drivers causing memory access errors
________________________________________
Step 2: Restart system
If faulty driver exists:
•	System will crash again (expected behavior)
•	Logs will identify the driver
________________________________________
Step 3: Fix driver
Open Device Manager:
devmgmt.msc
Then:
•	Locate faulty driver
•	Right-click → Roll Back Driver OR Update Driver
________________________________________
Outcome
Faulty driver replaced → system stabilised.
________________________________________
Learning
•	IRQL errors = almost always driver-related
•	Network and chipset drivers are common causes
________________________________________
4. PAGE_FAULT_IN_NONPAGED_AREA
What users experience
System crashes when opening applications or antivirus software.
________________________________________
Step-by-step troubleshooting
Step 1: Identify software conflict
Check recently installed apps:
•	Antivirus software
•	VPN tools
________________________________________
Step 2: Remove conflicting software
Go to:
Control Panel → Programs → Uninstall
________________________________________
Step 3: Repair system files
sfc /scannow
Explanation:
•	Fixes missing memory references
•	Repairs corrupted system access paths
________________________________________
Outcome
Conflicting software removed → stability restored.
________________________________________
Learning
•	Antivirus tools frequently conflict with memory management
________________________________________
5. SYSTEM_SERVICE_EXCEPTION
What users experience
Crash during login or while using applications.
________________________________________
Step-by-step troubleshooting
Step 1: Check GPU driver
Open:
devmgmt.msc
Go to:
•	Display Adapters
________________________________________
Step 2: Update driver
•	Right-click GPU
•	Select Update Driver
•	OR uninstall and reinstall latest version
________________________________________
Step 3: Check logs
eventvwr.msc
Look for:
•	“ntoskrnl.exe”
•	driver-related failures
________________________________________
Outcome
Updated GPU driver resolved BSOD.
________________________________________
Learning
Graphics drivers are highly sensitive to OS updates.
________________________________________
6. KERNEL_SECURITY_CHECK_FAILURE
What users experience
BSOD during startup or login due to security integrity violation.
________________________________________
Step-by-step troubleshooting
Step 1: Scan system integrity
sfc /scannow
Step 2: Repair Windows image
DISM /Online /Cleanup-Image /RestoreHealth
________________________________________
Step 3: Malware scan
Run:
•	Windows Defender Full Scan
________________________________________
Outcome
Corrupted kernel components repaired.
________________________________________
Learning
•	Kernel errors often caused by malware or driver corruption
________________________________________
7. BAD_POOL_CALLER
What users experience
System crashes when connecting USB devices.
________________________________________
Step-by-step troubleshooting
Step 1: Disconnect all USB devices
________________________________________
Step 2: Check Device Manager
devmgmt.msc
•	Look for warning icons
________________________________________
Step 3: Reinstall drivers
•	USB controllers → uninstall → restart
________________________________________
Outcome
USB driver reset fixes issue.
________________________________________
Learning
External devices can directly impact system memory pools.
________________________________________
8. DPC_WATCHDOG_VIOLATION
What users experience
System freezes and restarts, often during file transfers.
________________________________________
Step-by-step troubleshooting
Step 1: Check SSD health
Open:
•	Device Manager → Disk Drives
________________________________________
Step 2: Update firmware
•	Visit manufacturer tool (Samsung Magician, etc.)
________________________________________
Step 3: BIOS settings
•	Enter BIOS (F2/DEL)
•	Change SATA mode to AHCI
________________________________________
Outcome
Storage performance stabilised.
________________________________________
Learning
Storage firmware issues cause delayed system responses.
________________________________________
9. UNEXPECTED_STORE_EXCEPTION
What users experience
Crash during file access or startup.
________________________________________
Step-by-step troubleshooting
Step 1: Run disk check
chkdsk /f /r
What this does:
•	/f → fixes file system errors
•	/r → locates bad sectors and recovers data
________________________________________
Step 2: Restart system
•	Disk scan runs before Windows loads
________________________________________
Outcome
Faulty disk sectors repaired or disk replaced.
________________________________________
Learning
Storage failure is a leading cause of BSOD.
________________________________________
10. VIDEO_TDR_FAILURE
What users experience
Screen freezes then BSOD while gaming or using graphics apps.
________________________________________
Step-by-step troubleshooting
Step 1: Update GPU driver
________________________________________
Step 2: Adjust registry timeout
Run:
reg add "HKLM\System\CurrentControlSet\Control\GraphicsDrivers" /v TdrDelay /t REG_DWORD /d 10 /f
What this does:
•	Increases GPU response timeout
•	Prevents premature driver reset
________________________________________
Outcome
GPU stability restored.
________________________________________
Learning
•	GPU timeouts occur under heavy processing loads
________________________________________
Visual Troubleshooting Flow (Recommended GitHub Image)
📌 Add diagram as image file in GitHub
[BSOD Occurs]
      ↓
[Safe Mode Boot]
      ↓
[Event Viewer Analysis]
      ↓
[Driver or Hardware Identification]
      ↓
[SFC / DISM / CHKDSK]
      ↓
[Fix Applied]
      ↓
[System Validation]
________________________________________
Conclusion
Effective BSOD troubleshooting requires:
•	Structured diagnostic steps
•	Correct use of system tools
•	Driver and hardware validation
•	Log analysis using Event Viewer
This guide provides a real-world IT support workflow suitable for enterprise environments and GitHub portfolio documentation.

