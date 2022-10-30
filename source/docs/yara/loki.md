# Scanning with Loki

LOKI is a free open source IOC (Indicator of Compromise) scanner created/written by Florian Roth.

According to the [GitHub page](https://github.com/Neo23x0/Loki), detection is based on 4 methods:

1. File Name IOC Check - Regex match on full file path/name
2. Yara Rule Check - Yara signature match on file data and process memory
3. Hash Check - Compares known malicious hashes (MD5, SHA1, SHA256) with scanned files
4. C2 Back Connect Check - Compares process connection endpoints with C2 IOCs (new since version v.10)

LOKI can be used on both Windows and Linux systems for:

* Research threat intelligence reports, blog postings, etc. and gather information on the latest tactics and techniques 
used in the wild, past or present: IOCs (hashes, IP addresses, domain names, etc.) will be shared so rules can be 
created to detect these threats, along with Yara rules. 
* In situations with something unknown that the security stack of tools can't/didn't detect: Using tools such as 
Loki, add rules based on threat intelligence gathering or findings from an incident response engagement (forensics).

## Examples

Loki already has a set of Yara rules for start scanning for evil on an endpoint.

### File1

```text
$ sudo python loki.py -p ~/suspicious-files/file1/
[sudo] password for cmnatic: 
                                                                               
      __   ____  __ ______                            
     / /  / __ \/ //_/  _/                            
    / /__/ /_/ / ,< _/ /                              
   /____/\____/_/|_/___/                              
      ________  _____  ____                           
     /  _/ __ \/ ___/ / __/______ ____  ___  ___ ____ 
    _/ // /_/ / /__  _\ \/ __/ _ `/ _ \/ _ \/ -_) __/ 
   /___/\____/\___/ /___/\__/\_,_/_//_/_//_/\__/_/    

   Copyright by Florian Roth, Released under the GNU General Public License
   Version 0.32.1
  
   DISCLAIMER - USE AT YOUR OWN RISK
   Please report false positives via https://github.com/Neo23x0/Loki/issues
  
                                                                               

[NOTICE] Starting Loki Scan VERSION: 0.32.1 SYSTEM: thm-yara TIME: 20221030T00:38:10Z PLATFORM:     PROC: x86_64 ARCH: 64bit 
[NOTICE] Registered plugin PluginWMI
[NOTICE] Loaded plugin /home/cmnatic/tools/Loki/plugins/loki-plugin-wmi.py
[NOTICE] PE-Sieve successfully initialized BINARY: /home/cmnatic/tools/Loki/tools/pe-sieve64.exe SOURCE: https://github.com/hasherezade/pe-sieve
[INFO] File Name Characteristics initialized with 2841 regex patterns
[INFO] C2 server indicators initialized with 1541 elements
[INFO] Malicious MD5 Hashes initialized with 19034 hashes
[INFO] Malicious SHA1 Hashes initialized with 7159 hashes
[INFO] Malicious SHA256 Hashes initialized with 22841 hashes
[INFO] False Positive Hashes initialized with 30 hashes
[INFO] Processing YARA rules folder /home/cmnatic/tools/Loki/signature-base/yara
[INFO] Initializing all YARA rules at once (composed string of all rule files)
[INFO] Initialized 653 Yara rules
[INFO] Reading private rules from binary ...
[INFO] Current user is root - very good
[NOTICE] Running plugin PluginWMI
[NOTICE] Finished running plugin PluginWMI
[INFO] Scanning /home/cmnatic/suspicious-files/file1/ ...  
[WARNING] 
FILE: /home/cmnatic/suspicious-files/file1/ind3x.php SCORE: 70 TYPE: PHP SIZE: 80992 
FIRST_BYTES: 3c3f7068700a2f2a0a09623337346b20322e320a / <?php/*b374k 2.2 
MD5: 1606bdac2cb613bf0b8a22690364fbc5 
SHA1: 9383ed4ee7df17193f7a034c3190ecabc9000f9f 
SHA256: 5479f8cd1375364770df36e5a18262480a8f9d311e8eedb2c2390ecb233852ad CREATED: Mon Nov  9 15:15:32 2020 MODIFIED: Mon Nov  9 13:06:56 2020 ACCESSED: Sun Oct 30 00:35:44 2022 
REASON_1: Yara Rule MATCH: webshell_metaslsoft SUBSCORE: 70 
DESCRIPTION: Web Shell - file metaslsoft.php REF: - 
MATCHES: Str1: $buff .= "<tr><td><a href=\\"?d=".$pwd."\\">[ $folder ]</a></td><td>LINK</t
[NOTICE] Results: 0 alerts, 1 warnings, 6 notices
[RESULT] Suspicious objects detected!
[RESULT] Loki recommends a deeper analysis of the suspicious objects.
[INFO] Please report false positives via https://github.com/Neo23x0/signature-base
[NOTICE] Finished LOKI Scan SYSTEM: thm-yara TIME: 20221030T00:38:14Z
 
Press Enter to exit ...
```

### File2

```text
$ sudo python loki.py -p ~/suspicious-files/file2/
                                                                               
      __   ____  __ ______                            
     / /  / __ \/ //_/  _/                            
    / /__/ /_/ / ,< _/ /                              
   /____/\____/_/|_/___/                              
      ________  _____  ____                           
     /  _/ __ \/ ___/ / __/______ ____  ___  ___ ____ 
    _/ // /_/ / /__  _\ \/ __/ _ `/ _ \/ _ \/ -_) __/ 
   /___/\____/\___/ /___/\__/\_,_/_//_/_//_/\__/_/    

   Copyright by Florian Roth, Released under the GNU General Public License
   Version 0.32.1
  
   DISCLAIMER - USE AT YOUR OWN RISK
   Please report false positives via https://github.com/Neo23x0/Loki/issues
  
                                                                               

[NOTICE] Starting Loki Scan VERSION: 0.32.1 SYSTEM: thm-yara TIME: 20221030T00:42:24Z PLATFORM:     PROC: x86_64 ARCH: 64bit 
[NOTICE] Registered plugin PluginWMI
[NOTICE] Loaded plugin /home/cmnatic/tools/Loki/plugins/loki-plugin-wmi.py
[NOTICE] PE-Sieve successfully initialized BINARY: /home/cmnatic/tools/Loki/tools/pe-sieve64.exe SOURCE: https://github.com/hasherezade/pe-sieve
[INFO] File Name Characteristics initialized with 2841 regex patterns
[INFO] C2 server indicators initialized with 1541 elements
[INFO] Malicious MD5 Hashes initialized with 19034 hashes
[INFO] Malicious SHA1 Hashes initialized with 7159 hashes
[INFO] Malicious SHA256 Hashes initialized with 22841 hashes
[INFO] False Positive Hashes initialized with 30 hashes
[INFO] Processing YARA rules folder /home/cmnatic/tools/Loki/signature-base/yara
[INFO] Initializing all YARA rules at once (composed string of all rule files)
[INFO] Initialized 653 Yara rules
[INFO] Reading private rules from binary ...
[INFO] Current user is root - very good
[NOTICE] Running plugin PluginWMI
[NOTICE] Finished running plugin PluginWMI
[INFO] Scanning /home/cmnatic/suspicious-files/file2/ ...  
[NOTICE] Results: 0 alerts, 0 warnings, 6 notices
[RESULT] SYSTEM SEEMS TO BE CLEAN.
[INFO] Please report false positives via https://github.com/Neo23x0/signature-base
[NOTICE] Finished LOKI Scan SYSTEM: thm-yara TIME: 20221030T00:42:28Z
```

We have a file that Loki did not flag on and running Loki on other web servers is useless, because if `file 2` exists 
in any of the webs servers, it will go undetected.

The solution is to create a Yara rule to detect this specific web shell. Manually sifting through lines upon lines of 
code to find possible strings that can be used in a Yara rule can be daunting.

[yarGen](yargen.md) can be used in this case.
