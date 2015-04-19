
VolDiff: Malware Memory Footprint Analysis
==========================================

VolDiff is a malware analysis tool based on Volatility.

Directions:
-----------

1. Capture a memory dump of a clean Windows system and save it as "baseline.raw". This image will serve as a baseline for the analysis.

2. Execute your malware sample on the same system, then take a second memory dump and save it as "infected.raw".

3. Run VolDiff:
<pre>
./VolDiff.sh path/to/baseline.raw path/to/infected.raw profile
</pre>
"profile" should be "Win7SP0x86" or "Win7SP1x64" etc.

VolDiff will save the output of a selection of Volatility plugins for both memory images (baseline and infected), then create a report to highlight notable changes (new processes, network connections, injected code, drivers etc).

Tested using Volatility 2.4 (vol.py) and Windows 7 memory images.

Errors?
-----------

Please report bugs to houcem.hachicha[@]gmail.com.

Sample Output
---------------
<pre>
 _    __      ______  _ ________
| |  / /___  / / __ \(_) __/ __/
| | / / __ \/ / / / / / /_/ /_  
| |/ / /_/ / / /_/ / / __/ __/  
|___/\____/_/_____/_/_/ /_/     

Volatility analysis report generated by VolDiff v0.9.1 (https://github.com/houcem).

Suspicious new netscan entries
=========================================================================

Offset(P)          Proto    Local Address                  Foreign Address      State            Pid      Owner          Created
0x3da3f618         TCPv4    172.16.108.128:139             0.0.0.0:0            LISTENING        4        System         
0x3daeccf8         TCPv4    0.0.0.0:80                     0.0.0.0:0            LISTENING        2108     explorer.exe   
0x3dad8008         TCPv4    172.16.108.128:49167           62.24.131.168:80     CLOSED           924      svchost.exe    
0x3fc7b630         TCPv4    172.16.108.128:49164           65.55.50.157:443     CLOSED           924      svchost.exe    
0x3fc8b5f0         TCPv4    172.16.108.128:49165           62.24.131.168:80     CLOSED           924      svchost.exe    
0x3fdf2348         TCPv4    172.16.108.128:49168           87.236.215.151:80    CLOSED           2108     explorer.exe   


Suspicious new pslist entries
=========================================================================

Offset(V)  Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit                          
---------- -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0x855c9738 wuauclt.exe            3976    924      5       97      1      0 2015-04-18 22:58:09 UTC+0000                                 
0x872de0c0 cmd.exe                1184   1544      0 --------      0      0 2015-04-18 22:58:29 UTC+0000   2015-04-18 22:58:29 UTC+0000  
0x8510c980 ipconfig.exe           2544   1184      0 --------      0      0 2015-04-18 22:58:29 UTC+0000   2015-04-18 22:58:29 UTC+0000  
0x85123030 conhost.exe            2560    360      0 --------      0      0 2015-04-18 22:58:29 UTC+0000   2015-04-18 22:58:29 UTC+0000  
0x8510c980 ipconfig.exe           2544   1184      0 --------      0      0 2015-04-18 22:58:29 UTC+0000   2015-04-18 22:58:29 UTC+0000  


Suspicious new psscan entries
=========================================================================

Offset(P)          Name                PID   PPID PDB        Time created                   Time exited                   
------------------ ---------------- ------ ------ ---------- ------------------------------ ------------------------------
0x000000003dade0c0 cmd.exe            1184   1544 0x3ee13380 2015-04-18 22:58:29 UTC+0000   2015-04-18 22:58:29 UTC+0000  
0x000000003fd0c980 ipconfig.exe       2544   1184 0x3ee135c0 2015-04-18 22:58:29 UTC+0000   2015-04-18 22:58:29 UTC+0000  
0x000000003f9c9738 wuauclt.exe        3976    924 0x3ee134e0 2015-04-18 22:58:09 UTC+0000                                 
0x000000003fd0c980 ipconfig.exe       2544   1184 0x3ee135c0 2015-04-18 22:58:29 UTC+0000   2015-04-18 22:58:29 UTC+0000  
0x000000003fd23030 conhost.exe        2560    360 0x3ee13500 2015-04-18 22:58:29 UTC+0000   2015-04-18 22:58:29 UTC+0000  

Suspicious new ldrmodules entries
=========================================================================

Pid      Process              Base       InLoad InInit InMem MappedPath
-------- -------------------- ---------- ------ ------ ----- ----------
     360 csrss.exe            0x4a040000 True   False  True  \Windows\System32\csrss.exe
     424 csrss.exe            0x011a0000 False  False  False \Windows\Fonts\vga850.fon
    1096 svchost.exe          0x00220000 True   False  True  \Windows\System32\svchost.exe
    1324 spoolsv.exe          0x009d0000 False  False  False \Windows\System32\spool\drivers\w32x86\3\fr-FR\PS5UI.DLL.mui
    2108 explorer.exe         0x04990000 False  False  False \Windows\System32\fr-FR\crypt32.dll.mui
    2108 explorer.exe         0x020b0000 False  False  False \Windows\System32\fr-FR\mpr.dll.mui
    2108 explorer.exe         0x040b0000 False  False  False \Windows\System32\fr-FR\urlmon.dll.mui
    2108 explorer.exe         0x06b80000 False  False  False \Windows\System32\imageres.dll
    2108 explorer.exe         0x04a70000 False  False  False \Windows\System32\fr-FR\oleaccrc.dll.mui
    2108 explorer.exe         0x03690000 False  False  False \Windows\System32\fr-FR\user32.dll.mui
    2108 explorer.exe         0x02280000 False  False  False \Windows\System32\fr-FR\shdocvw.dll.mui
    2108 explorer.exe         0x046e0000 False  False  False \Windows\System32\fr-FR\KernelBase.dll.mui
    2108 explorer.exe         0x03700000 False  False  False \Windows\System32\fr-FR\winmm.dll.mui
    2108 explorer.exe         0x02270000 False  False  False \Windows\System32\fr-FR\imageres.dll.mui
    3976 wuauclt.exe          0x00ac0000 True   False  True  \Windows\System32\wuauclt.exe
    3976 wuauclt.exe          0x00100000 False  False  False \Windows\System32\oleaccrc.dll
    3976 wuauclt.exe          0x00310000 False  False  False \Windows\System32\fr-FR\wucltux.dll.mui


Suspicious new malfind entries
=========================================================================

Process: explorer.exe Pid: 2108 Address: 0x22f0000
Vad Tag: VadS Protection: PAGE_EXECUTE_READWRITE
Flags: CommitCharge: 2, MemCommit: 1, PrivateMemory: 1, Protection: 6

0x022f0000  4d 5a 00 00 00 00 00 00 00 00 00 00 00 00 00 00   MZ..............
0x022f0010  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0x022f0020  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0x022f0030  00 00 00 00 00 00 00 00 00 00 00 00 40 00 00 00   ............@...

0x22f0000 4d               DEC EBP
0x22f0001 5a               POP EDX
0x22f0002 0000             ADD [EAX], AL
0x22f0004 0000             ADD [EAX], AL
0x22f0006 0000             ADD [EAX], AL
0x22f0008 0000             ADD [EAX], AL
0x22f000a 0000             ADD [EAX], AL
0x22f000c 0000             ADD [EAX], AL
0x22f000e 0000             ADD [EAX], AL
0x22f0010 0000             ADD [EAX], AL
0x22f0012 0000             ADD [EAX], AL
0x22f0014 0000             ADD [EAX], AL
0x22f0016 0000             ADD [EAX], AL
0x22f0018 0000             ADD [EAX], AL
0x22f001a 0000             ADD [EAX], AL
0x22f001c 0000             ADD [EAX], AL
0x22f001e 0000             ADD [EAX], AL
0x22f0020 0000             ADD [EAX], AL
0x22f0022 0000             ADD [EAX], AL
0x22f0024 0000             ADD [EAX], AL
0x22f0026 0000             ADD [EAX], AL
0x22f0028 0000             ADD [EAX], AL
0x22f002a 0000             ADD [EAX], AL
0x22f002c 0000             ADD [EAX], AL
0x22f002e 0000             ADD [EAX], AL
0x22f0030 0000             ADD [EAX], AL
0x22f0032 0000             ADD [EAX], AL
0x22f0034 0000             ADD [EAX], AL
0x22f0036 0000             ADD [EAX], AL
0x22f0038 0000             ADD [EAX], AL
0x22f003a 0000             ADD [EAX], AL
0x22f003c 40               INC EAX
0x22f003d 0000             ADD [EAX], AL
0x22f003f 00               DB 0x0


Process: explorer.exe Pid: 2108 Address: 0x10060000
Vad Tag: VadS Protection: PAGE_EXECUTE_READWRITE
Flags: CommitCharge: 65537, MemCommit: 1, PrivateMemory: 1, Protection: 6

0x10060000  55 89 e5 53 57 56 81 ec 9c 01 00 00 8b 45 08 c7   U..SWV.......E..
0x10060010  45 ec 04 00 00 00 8b 4d ec c7 45 c0 01 00 00 00   E......M..E.....
0x10060020  8b 55 c0 c7 85 e8 fe ff ff 01 00 00 00 8b b5 e8   .U..............
0x10060030  fe ff ff c7 85 18 ff ff ff 20 00 00 00 c6 85 53   ...............S

0x10060000 55               PUSH EBP
0x10060001 89e5             MOV EBP, ESP
0x10060003 53               PUSH EBX
0x10060004 57               PUSH EDI
0x10060005 56               PUSH ESI
0x10060006 81ec9c010000     SUB ESP, 0x19c
0x1006000c 8b4508           MOV EAX, [EBP+0x8]
0x1006000f c745ec04000000   MOV DWORD [EBP-0x14], 0x4
0x10060016 8b4dec           MOV ECX, [EBP-0x14]
0x10060019 c745c001000000   MOV DWORD [EBP-0x40], 0x1
0x10060020 8b55c0           MOV EDX, [EBP-0x40]
0x10060023 c785e8feffff01000000 MOV DWORD [EBP-0x118], 0x1
0x1006002d 8bb5e8feffff     MOV ESI, [EBP-0x118]
0x10060033 c78518ffffff20000000 MOV DWORD [EBP-0xe8], 0x20
0x1006003d c6               DB 0xc6
0x1006003e 85               DB 0x85
0x1006003f 53               PUSH EBX


Suspicious new timeliner entries
=========================================================================

1970-01-01 00:00:00 UTC+0000|[NETWORK CONNECTION]| 0.0.0.0:80 -> 0.0.0.0:0| 2108/TCPv4/LISTENING/0x3daeccf8
1970-01-01 00:00:00 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:139 -> 0.0.0.0:0| 4/TCPv4/LISTENING/0x3da3f618
1970-01-01 00:00:00 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:49164 -> 65.55.50.157:443| 924/TCPv4/CLOSED/0x3fc7b630
1970-01-01 00:00:00 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:49165 -> 62.24.131.168:80| 924/TCPv4/CLOSED/0x3fc8b5f0
1970-01-01 00:00:00 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:49167 -> 62.24.131.168:80| 924/TCPv4/CLOSED/0x3dad8008
1970-01-01 00:00:00 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:49168 -> 87.236.215.151:80| 2108/TCPv4/CLOSED/0x3fdf2348
2009-06-04 05:25:08 UTC+0000|[PE HEADER (exe)]| mscorsvw.exe| Process: mscorsvw.exe/PID: 3176/PPID: 508/Process POffset: 0x3e135538/DLL Base: 0x10000000
2009-07-13 23:11:23 UTC+0000|[PE HEADER (exe)]| services.exe| Process: services.exe/PID: 508/PPID: 412/Process POffset: 0x2594c3a8/DLL Base: 0x00200000
2009-07-13 23:19:28 UTC+0000|[PE HEADER (exe)]| svchost.exe| Process: svchost.exe/PID: 640/PPID: 508/Process POffset: 0x3e072c48/DLL Base: 0x00220000
2009-07-13 23:25:37 UTC+0000|[PE HEADER (exe)]| conhost.exe| Process: conhost.exe/PID: 2184/PPID: 424/Process POffset: 0x3da32030/DLL Base: 0x00ce0000
2009-07-13 23:37:00 UTC+0000|[PE HEADER (exe)]| winlogon.exe| Process: winlogon.exe/PID: 480/PPID: 404/Process POffset: 0x3e368628/DLL Base: 0x00120000
2009-07-14 00:02:42 UTC+0000|[PE HEADER (exe)]| lsm.exe| Process: lsm.exe/PID: 524/PPID: 412/Process POffset: 0x3e014030/DLL Base: 0x00f30000
2012-06-02 22:12:17 UTC+0000|[PE HEADER (exe)]| wuauclt.exe| Process: wuauclt.exe/PID: 3976/PPID: 924/Process POffset: 0x3f9c9738/DLL Base: 0x00ac0000
2015-02-06 22:03:09 UTC+0000|[PE HEADER (exe)]| vmtoolsd.exe| Process: vmtoolsd.exe/PID: 1544/PPID: 508/Process POffset: 0x3e178130/DLL Base: 0x00140000
2015-04-18 22:49:24 UTC+0000|[PROCESS]| lsm.exe| PID: 524/PPID: 412/POffset: 0x3e014030
2015-04-18 22:49:24 UTC+0000|[PROCESS]| services.exe| PID: 508/PPID: 412/POffset: 0x2594c3a8
2015-04-18 22:49:24 UTC+0000|[PROCESS]| winlogon.exe| PID: 480/PPID: 404/POffset: 0x3e368628
2015-04-18 22:49:25 UTC+0000|[PROCESS]| svchost.exe| PID: 640/PPID: 508/POffset: 0x3e072c48
2015-04-18 22:49:26 UTC+0000|[PROCESS]| vmtoolsd.exe| PID: 1544/PPID: 508/POffset: 0x3e178130
2015-04-18 22:49:27 UTC+0000|[PROCESS]| TPAutoConnSvc.| PID: 1792/PPID: 508/POffset: 0x3e1bbd40
2015-04-18 22:49:32 UTC+0000|[PROCESS]| conhost.exe| PID: 2184/PPID: 424/POffset: 0x3da32030
2015-04-18 22:49:32 UTC+0000|[PROCESS]| explorer.exe| PID: 2108/PPID: 2084/POffset: 0x3da16828
2015-04-18 22:51:27 UTC+0000|[PROCESS]| mscorsvw.exe| PID: 3176/PPID: 508/POffset: 0x3e135538
2015-04-18 22:56:42 UTC+0000|[NETWORK CONNECTION]| fe80::2587:a98d:6d2c:9d30:546 -> *:*| 756/UDPv6//0x3fd00008
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| ::1:1900 -> *:*| 3140/UDPv6//0x3df328f0
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| 127.0.0.1:1900 -> *:*| 3140/UDPv4//0x3f930008
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| 127.0.0.1:58120 -> *:*| 3140/UDPv4//0x3fce9008
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| ::1:58118 -> *:*| 3140/UDPv6//0x3f930a58
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:137 -> *:*| 4/UDPv4//0x3fac8640
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:138 -> *:*| 4/UDPv4//0x3da0e2d0
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:1900 -> *:*| 3140/UDPv4//0x3e1db610
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:58119 -> *:*| 3140/UDPv4//0x3fc51990
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| fe80::2587:a98d:6d2c:9d30:1900 -> *:*| 3140/UDPv6//0x3dc2ec70
2015-04-18 22:56:43 UTC+0000|[NETWORK CONNECTION]| fe80::2587:a98d:6d2c:9d30:58117 -> *:*| 3140/UDPv6//0x3fdc2e98
2015-04-18 22:58:09 UTC+0000|[PROCESS]| wuauclt.exe| PID: 3976/PPID: 924/POffset: 0x3f9c9738
2015-04-18 22:58:29 UTC+0000|[NETWORK CONNECTION]| 0.0.0.0:0 -> *:*| 1232/UDPv4//0x3f297f50
2015-04-18 22:58:29 UTC+0000|[NETWORK CONNECTION]| 0.0.0.0:5355 -> *:*| 1232/UDPv4//0x3f9346f8
2015-04-18 22:58:29 UTC+0000|[NETWORK CONNECTION]| 0.0.0.0:5355 -> *:*| 1232/UDPv4//0x3fac7110
2015-04-18 22:58:29 UTC+0000|[NETWORK CONNECTION]| :::0 -> *:*| 1232/UDPv6//0x3f297f50
2015-04-18 22:58:29 UTC+0000|[NETWORK CONNECTION]| 172.16.108.128:68 -> *:*| 756/UDPv4//0x3faa0238
2015-04-18 22:58:29 UTC+0000|[NETWORK CONNECTION]| :::5355 -> *:*| 1232/UDPv6//0x3f9346f8
2015-04-18 22:58:29 UTC+0000|[PROCESS]| cmd.exe| PID: 1184/PPID: 1544/POffset: 0x3dade0c0 End: 2015-04-18 22:58:29 UTC+0000
2015-04-18 22:58:29 UTC+0000|[PROCESS]| conhost.exe| PID: 2560/PPID: 360/POffset: 0x3fd23030 End: 2015-04-18 22:58:29 UTC+0000
2015-04-18 22:58:29 UTC+0000|[PROCESS]| ipconfig.exe| PID: 2544/PPID: 1184/POffset: 0x3fd0c980 End: 2015-04-18 22:58:29 UTC+0000


Suspicious new svcscan entries
=========================================================================

Process ID: -
Service State: SERVICE_STOPPED
Binary Path: -
Process ID: 876
Service State: SERVICE_RUNNING
Binary Path: C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted
Process ID: 924
Service State: SERVICE_RUNNING
Binary Path: C:\Windows\system32\svchost.exe -k netsvcs


Suspicious new cmdline entries
=========================================================================

wuauclt.exe pid:   3976
Command line : "C:\Windows\system32\wuauclt.exe"
************************************************************************
cmd.exe pid:   1184
conhost.exe pid:   2560
ipconfig.exe pid:   2544

Suspicious new mutantscan entries
=========================================================================

Offset(P)              #Ptr     #Hnd Signal Thread           CID Name
------------------ -------- -------- ------ ---------- --------- ----
0x000000003da022f8        3        2      1 0x00000000           HGFSMUTEX
0x000000003da3e120        2        1      1 0x00000000           5827a689a8a470200835d840817112f0
0x000000003daaab90        2        1      1 0x00000000           WininetProxyRegistryMutex
0x000000003df68d60        2        1      0 0x855d8248 2108:1140 41df362a3f3d701bb5b5749a3e43f484
0x000000003e171b68        5        4      1 0x00000000           d3b1bbc7-c020-4056-9ded-7c6f40b5a2fc
0x000000003f984208        2        1      0 0x852c41d0 2108:3712 ad1751de900a1713cecd716adfda611f
0x000000003f99a228        2        1      1 0x00000000           WininetStartupMutex
0x000000003f9ddef8        2        1      0 0x872aabe0  2108:668 cb16681dee85a67993f0759da19566be
0x000000003fcd69a0        2        1      1 0x00000000           WininetConnectionMutex
0x000000003fd4dcd8        4        3      1 0x00000000           C::Users:victim:AppData:Local:Microsoft:Windows:Explorer:thumbcache_1024.db!dfMaintainer
0x000000003fd4dd38        4        3      1 0x00000000           C::Users:victim:AppData:Local:Microsoft:Windows:Explorer:thumbcache_256.db!dfMaintainer
0x000000003fd4dd98        4        3      1 0x00000000           C::Users:victim:AppData:Local:Microsoft:Windows:Explorer:thumbcache_96.db!dfMaintainer
0x000000003fd886b0        4        3      1 0x00000000           C::Users:victim:AppData:Local:Microsoft:Windows:Explorer:thumbcache_idx.db!ThumbnailCacheInit
0x000000003fd88710        4        3      1 0x00000000           C::Users:victim:AppData:Local:Microsoft:Windows:Explorer:thumbcache_sr.db!dfMaintainer
0x000000003fdd7438        2        1      1 0x00000000           _!MSFTHISTORY!_
C::Users:victim:AppData:Local:Microsoft:Windows:Explorer:thumbcache_idx.db!rwWriterMutex

Suspicious new getsids entries
=========================================================================

wuauclt.exe (3976): S-1-5-21-2921091077-2763243831-321783825-1000 (victim)
wuauclt.exe (3976): S-1-5-21-2921091077-2763243831-321783825-513 (Domain Users)
wuauclt.exe (3976): S-1-1-0 (Everyone)
wuauclt.exe (3976): S-1-5-32-544 (Administrators)
wuauclt.exe (3976): S-1-5-32-545 (Users)
wuauclt.exe (3976): S-1-5-4 (Interactive)
wuauclt.exe (3976): S-1-2-1 (Console Logon (Users who are logged onto the physical console))
wuauclt.exe (3976): S-1-5-11 (Authenticated Users)
wuauclt.exe (3976): S-1-5-15 (This Organization)
wuauclt.exe (3976): S-1-5-5-0-276475 (Logon Session)
wuauclt.exe (3976): S-1-2-0 (Local (Users with the ability to log in locally))
wuauclt.exe (3976): S-1-5-64-10 (NTLM Authentication)
wuauclt.exe (3976): S-1-16-8192 (Medium Mandatory Level)
cmd.exe (1184): S-1-5-18 (Local System)
cmd.exe (1184): S-1-5-32-544 (Administrators)
cmd.exe (1184): S-1-1-0 (Everyone)
cmd.exe (1184): S-1-5-11 (Authenticated Users)
cmd.exe (1184): S-1-16-16384 (System Mandatory Level)
conhost.exe (2560): S-1-5-18 (Local System)
conhost.exe (2560): S-1-5-32-544 (Administrators)
conhost.exe (2560): S-1-1-0 (Everyone)
conhost.exe (2560): S-1-5-11 (Authenticated Users)
conhost.exe (2560): S-1-16-16384 (System Mandatory Level)
ipconfig.exe (2544): S-1-5-18 (Local System)
ipconfig.exe (2544): S-1-5-32-544 (Administrators)
ipconfig.exe (2544): S-1-1-0 (Everyone)
ipconfig.exe (2544): S-1-5-11 (Authenticated Users)
ipconfig.exe (2544): S-1-16-16384 (System Mandatory Level)

End of report.

</pre>
