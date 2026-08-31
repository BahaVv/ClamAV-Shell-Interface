# ClamAV-Shell-Interface
A basic shell interface for clamav scans on Linux. Written on Fedora 44, should work on any system with dnf that has clamav in the repos, but Your Mileage May Vary.

The script can be run through the shell, or it can be 'installed' as an application in pretty much any DE by just dropping the `ClamScan` folder into the `~/.local/share/applications/` directory.

Make sure the shell script is set as executable! This can be done through a terminal or through the file properties in the right-click menu of most file managers.

Upon launching (which requires root permissions), the script will ensure that all components for clamav are installed, create the log directory if not found, and then prompt the user for both how verbose the output should be, and what type of scan they would like. It will then run the scan! If only infected files are being reported, you'll likely be waiting a long time with no visible activity.

Current supported scan types are:

- Just the Downloads folder
- All folders in /home/
- Various system folders ( `/etc/`, `/tmp/`, `/var/tmp/`, `/opt/`, `/srv/`, `/bin/`, `/sbin/`, `/usr/local/bin/` )  
- Standard mounted drives ( in `/run/media` )
- All of the above, sequentially


Feature ideas:
- Checking log files for infected files and displaying them to the user after scan
- Optionally creating a crontab entry for scans or configuring the clamav daemon
- Parallel scans for "everything" scans
- A "keep alive" function showing that the scan is still running when in low-verbosity mode
- Prompting sudo on the terminal to avoid the scary password prompt when launching from GUI
- Debian-based and Arch-based distribution support (e.g. Ubuntu, CachyOS)


Sample output:
```
Checking to make sure ClamAV is installed...
ClamAV is installed!
Updating ClamAV definitions!
ClamAV update process started at Mon Aug 31 19:32:27 2026
daily.cld database is up-to-date (version: 28109, sigs: 355631, f-level: 90, builder: svc.clamav-publisher)
main.cvd database is up-to-date (version: 63, sigs: 3287027, f-level: 90, builder: tomjudge)
bytecode.cvd database is up-to-date (version: 339, sigs: 80, f-level: 90, builder: nrandolp)
Definitions updated.
Scans will be logged to /var/log/clamav

Please select output. This will also control what shows in log files:
[1] Infected files only
[2] All scanned files
What level of output would you like? [1 or 2]: 2

Please select a scan:
[1] Scan Downloads
[2] Scan home folders
[3] Scan system folders
[4] Scan all drives mounted in /run/media/ (Slow!)
[5] Scan everything (VERY slow!)
What scan would you like? [1, 2, 3, 4, or 5]: 1
Deleting oldest log file to avoid exceeding maximum number of logs (20)...

Log will be saved to /var/log/clamav/clamscan-download-20260831_1932.log

Beginning scan of Downloads...
/home/baha/Downloads/hello-world.dat: OK

----------- SCAN SUMMARY -----------
Known viruses: 3628036
Engine version: 1.4.6
Scanned directories: 1
Scanned files: 1
Infected files: 0
Data scanned: 0.00 MB
Data read: 0.00 MB (ratio 0.00:1)
Time: 12.953 sec (0 m 12 s)
Start Date: 2026:08:31 19:32:32
End Date:   2026:08:31 19:32:45

Downloads scan completed without issue!

All scans completed!

Log files created by scan:
/var/log/clamav/clamscan-download-20260831_1932.log
Press any key to exit...
```
