
# 1. CRITICAL_PROCESS_DIED

## What the user experiences

The system suddenly crashes and restarts. Windows displays a blue screen indicating that a critical system process has stopped unexpectedly.

---

## Step-by-step troubleshooting

### Step 1: Boot into Safe Mode

Safe Mode loads Windows with minimal drivers, allowing diagnosis without interference.

**How to do it:**

1. Restart PC
2. Hold **Shift + Restart**
3. Navigate to:

   * Troubleshoot → Advanced Options → Startup Settings
4. Press **F4 (Safe Mode)**

📌 *Image suggestion: Safe Mode menu screen*

---

### Step 2: Check system logs

Open Event Viewer:

```
eventvwr.msc
```

Go to:

* Windows Logs → System

Look for:

* Critical errors (red icons)
* “CRITICAL_PROCESS_DIED”

📌 This identifies what service failed.

---

### Step 3: Repair system files

Run Command Prompt as Administrator:

```
sfc /scannow
```

### What this does:

* Scans all protected system files
* Replaces corrupted or missing Windows files automatically

Then run:

```
DISM /Online /Cleanup-Image /RestoreHealth
```

### What this does:

* Repairs Windows image itself (deeper repair than SFC)
* Fixes corrupted update or system components

---

## Outcome

System files repaired, system stability restored.

---

## Learning

Most critical process failures are caused by:

* Corrupted Windows updates
* Failed system file updates
* Malware interference

---

# 2. MEMORY_MANAGEMENT

## What users experience

Random restarts or BSOD during heavy usage or startup.

---

## Step-by-step troubleshooting

### Step 1: Run Memory Diagnostic Tool

Press:

```
Windows Key + R
```

Type:

```
mdsched.exe
```

### What happens:

* System restarts
* RAM is tested before Windows loads
* Reports errors after reboot

📌 *Image suggestion: Windows Memory Diagnostic screen*

---

### Step 2: Interpret results

After reboot:

* Open Event Viewer
* Navigate to:

  ```
  Windows Logs → System
  ```
* Look for **MemoryDiagnostics-Results**

---

### Step 3: Hardware check

* Power off PC
* Remove RAM sticks
* Re-seat RAM into slots

---

## Outcome

Faulty RAM replaced or reseated → issue resolved.

---

## Learning

* RAM issues often mimic software crashes
* Hardware validation is essential before software fixes

---

# 3. IRQL_NOT_LESS_OR_EQUAL

## What users experience

Sudden BSOD when opening apps or connecting devices.

---

## Step-by-step troubleshooting

### Step 1: Enable Driver Verifier

Run Command Prompt as Admin:

```
verifier
```

Select:

* Create standard settings
* Select all drivers

### What this does:

* Forces Windows to check driver behavior
* Identifies unstable drivers causing memory access errors

---

### Step 2: Restart system

If faulty driver exists:

* System will crash again (expected behavior)
* Logs will identify the driver

---

### Step 3: Fix driver

Open Device Manager:

```
devmgmt.msc
```

Then:

* Locate faulty driver
* Right-click → Roll Back Driver OR Update Driver

---

## Outcome

Faulty driver replaced → system stabilised.

---

## Learning

* IRQL errors = almost always driver-related
* Network and chipset drivers are common causes

---

# 4. PAGE_FAULT_IN_NONPAGED_AREA

## What users experience

System crashes when opening applications or antivirus software.

---

## Step-by-step troubleshooting

### Step 1: Identify software conflict

Check recently installed apps:

* Antivirus software
* VPN tools

---

### Step 2: Remove conflicting software

Go to:

```
Control Panel → Programs → Uninstall
```

---

### Step 3: Repair system files

```
sfc /scannow
```

### Explanation:

* Fixes missing memory references
* Repairs corrupted system access paths

---

## Outcome

Conflicting software removed → stability restored.

---

## Learning

* Antivirus tools frequently conflict with memory management

---

# 5. SYSTEM_SERVICE_EXCEPTION

## What users experience

Crash during login or while using applications.

---

## Step-by-step troubleshooting

### Step 1: Check GPU driver

Open:

```
devmgmt.msc
```

Go to:

* Display Adapters

---

### Step 2: Update driver

* Right-click GPU
* Select Update Driver
* OR uninstall and reinstall latest version

---

### Step 3: Check logs

```
eventvwr.msc
```

Look for:

* “ntoskrnl.exe”
* driver-related failures

---

## Outcome

Updated GPU driver resolved BSOD.

---

## Learning

Graphics drivers are highly sensitive to OS updates.

---

# 6. KERNEL_SECURITY_CHECK_FAILURE

## What users experience

BSOD during startup or login due to security integrity violation.

---

## Step-by-step troubleshooting

### Step 1: Scan system integrity

```
sfc /scannow
```

### Step 2: Repair Windows image

```
DISM /Online /Cleanup-Image /RestoreHealth
```

---

### Step 3: Malware scan

Run:

* Windows Defender Full Scan

---

## Outcome

Corrupted kernel components repaired.

---

## Learning

* Kernel errors often caused by malware or driver corruption

---

# 7. BAD_POOL_CALLER

## What users experience

System crashes when connecting USB devices.

---

## Step-by-step troubleshooting

### Step 1: Disconnect all USB devices

---

### Step 2: Check Device Manager

```
devmgmt.msc
```

* Look for warning icons

---

### Step 3: Reinstall drivers

* USB controllers → uninstall → restart

---

## Outcome

USB driver reset fixes issue.

---

## Learning

External devices can directly impact system memory pools.

---

# 8. DPC_WATCHDOG_VIOLATION

## What users experience

System freezes and restarts, often during file transfers.

---

## Step-by-step troubleshooting

### Step 1: Check SSD health

Open:

* Device Manager → Disk Drives

---

### Step 2: Update firmware

* Visit manufacturer tool (Samsung Magician, etc.)

---

### Step 3: BIOS settings

* Enter BIOS (F2/DEL)
* Change SATA mode to AHCI

---

## Outcome

Storage performance stabilised.

---

## Learning

Storage firmware issues cause delayed system responses.

---

# 9. UNEXPECTED_STORE_EXCEPTION

## What users experience

Crash during file access or startup.

---

## Step-by-step troubleshooting

### Step 1: Run disk check

```
chkdsk /f /r
```

### What this does:

* /f → fixes file system errors
* /r → locates bad sectors and recovers data

---

### Step 2: Restart system

* Disk scan runs before Windows loads

---

## Outcome

Faulty disk sectors repaired or disk replaced.

---

## Learning

Storage failure is a leading cause of BSOD.

---

# 10. VIDEO_TDR_FAILURE

## What users experience

Screen freezes then BSOD while gaming or using graphics apps.

---

## Step-by-step troubleshooting

### Step 1: Update GPU driver

---

### Step 2: Adjust registry timeout

Run:

```
reg add "HKLM\System\CurrentControlSet\Control\GraphicsDrivers" /v TdrDelay /t REG_DWORD /d 10 /f
```

### What this does:

* Increases GPU response timeout
* Prevents premature driver reset

---

## Outcome

GPU stability restored.

---

## Learning

* GPU timeouts occur under heavy processing loads

---

# Conclusion

Effective BSOD troubleshooting requires:

* Structured diagnostic steps
* Correct use of system tools
* Driver and hardware validation
* Log analysis using Event Viewer

This guide provides a **real-world IT support workflow suitable for enterprise environments and GitHub portfolio documentation**.
