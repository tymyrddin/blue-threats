# Creating Yara rules with yarGen

yarGen is a generator for YARA rules.

From the README - _"The main principle is the creation of yara rules from strings found in malware files while removing all strings that also appear in goodware files. Therefore yarGen includes a big goodware strings and opcode database as ZIP archives that have to be extracted before the first use."_

## Example

Generate a Yara rule for suspicious `file 2`:

* `-m` is the path to the files you want to generate rules for
* `--excludegood force` to exclude all goodware strings (these are strings found in legitimate software and can increase false positives)
* `-o` location & name you want to output the Yara rule

```text
$ sudo python3 yarGen.py -m /home/cmnatic/suspicious-files/file2 --excludegood -o /home/cmnatic/suspicious-files/file2.yar
------------------------------------------------------------------------
                   _____            
    __ _____ _____/ ___/__ ___      
   / // / _ `/ __/ (_ / -_) _ \     
   \_, /\_,_/_/  \___/\__/_//_/     
  /___/  Yara Rule Generator        
         Florian Roth, July 2020, Version 0.23.3
   
  Note: Rules have to be post-processed
  See this post for details: https://medium.com/@cyb3rops/121d29322282
------------------------------------------------------------------------
[+] Using identifier 'file2'
[+] Using reference 'https://github.com/Neo23x0/yarGen'
[+] Using prefix 'file2'
[+] Processing PEStudio strings ...
[+] Reading goodware strings from database 'good-strings.db' ...
    (This could take some time and uses several Gigabytes of RAM depending on your db size)
[+] Loading ./dbs/good-imphashes-part9.db ...
[+] Total: 1 / Added 1 entries
[+] Loading ./dbs/good-exports-part6.db ...
[+] Total: 8065 / Added 8065 entries
[+] Loading ./dbs/good-imphashes-part2.db ...
...
[+] Loading ./dbs/good-strings-part7.db ...
[+] Total: 12284943 / Added 851561 entries
[+] Processing malware files ...
[+] Processing /home/cmnatic/suspicious-files/file2/1ndex.php ...
[+] Generating statistical data ...
[+] Generating Super Rules ... (a lot of foo magic)
[+] Generating Simple Rules ...
[-] Applying intelligent filters to string findings ...
[-] Filtering string set for /home/cmnatic/suspicious-files/file2/1ndex.php ...
[=] Generated 1 SIMPLE rules.
[=] All rules written to /home/cmnatic/suspicious-files/file2.yar
[+] yarGen run finished
```

Examine the generated Yara rule and remove any strings that you feel might generate false positives. If need be, 
use [yarAnalyzer](https://github.com/Neo23x0/yarAnalyzer/).

From within the root of the `suspicious files` directory, to test Yara and the generated Yara rule against `file 2`:

    yara file2.yar file2/1ndex.php

Now it is flagged.

Copy the generated Yara rule into the Loki signatures directory:

    ~/suspicious-files$ cp file2.yar ~/tools/Loki/signature-base/yara

Test the Yara rule with Loki:

```text
$ sudo python ~/tools/Loki/loki.py -p ~/suspicious-files/file2
                                                                               
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
  
                                                                               

[NOTICE] Starting Loki Scan VERSION: 0.32.1 SYSTEM: thm-yara TIME: 20221030T00:52:53Z PLATFORM:     PROC: x86_64 ARCH: 64bit 
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
[INFO] Initialized 654 Yara rules
[INFO] Reading private rules from binary ...
[INFO] Current user is root - very good
[NOTICE] Running plugin PluginWMI
[NOTICE] Finished running plugin PluginWMI
[INFO] Scanning /home/cmnatic/suspicious-files/file2 ...  
[WARNING] 
FILE: /home/cmnatic/suspicious-files/file2/1ndex.php SCORE: 70 TYPE: PHP SIZE: 223978 
FIRST_BYTES: 3c3f7068700a2f2a0a09623337346b207368656c / <?php/*b374k shel 
MD5: c6a7ebafdbe239d65248e2b69b670157 
SHA1: 3926ab64dcf04e87024011cf39902beac32711da 
SHA256: 53fe44b4753874f079a936325d1fdc9b1691956a29c3aaf8643cdbd49f5984bf CREATED: Mon Nov  9 15:16:03 2020 MODIFIED: Mon Nov  9 13:09:18 2020 ACCESSED: Sun Oct 30 00:42:28 2022 
REASON_1: Yara Rule MATCH: _home_cmnatic_suspicious_files_file2_1ndex SUBSCORE: 70 
DESCRIPTION: file2 - file 1ndex.php REF: https://github.com/Neo23x0/yarGen 
MATCHES: Str1: var Zepto=function(){function G(a){return a==null?String(a):z[A.call(a)]||"object"}function H(a){return G(a)=="function"}fun Str2: re ... (truncated)
[NOTICE] Results: 0 alerts, 1 warnings, 6 notices
[RESULT] Suspicious objects detected!
[RESULT] Loki recommends a deeper analysis of the suspicious objects.
[INFO] Please report false positives via https://github.com/Neo23x0/signature-base
[NOTICE] Finished LOKI Scan SYSTEM: thm-yara TIME: 20221030T00:52:57Z
 
Press Enter to exit ...
```

## Resources

* [How to Write Simple but Sound Yara Rules](https://www.bsk-consulting.de/2015/02/16/write-simple-sound-yara-rules/)
* [How to Write Simple but Sound Yara Rules – Part 2](https://www.bsk-consulting.de/2015/10/17/how-to-write-simple-but-sound-yara-rules-part-2/)
* [How to Write Simple but Sound Yara Rules – Part 3](https://www.bsk-consulting.de/2016/04/15/how-to-write-simple-but-sound-yara-rules-part-3/)