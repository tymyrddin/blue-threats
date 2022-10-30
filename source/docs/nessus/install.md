# Installation on Debian/Kali and Ubuntu

1. Goto [Tenable: Nessus Essentials](https://www.tenable.com/products/nessus/nessus-essentials) and register an account 
to get an activation code.

2. Download the `Nessus-#.##.#-debian6_amd64.deb` file and install:

```text
sudo dpkg -i <the package_file.deb filename>
```

3. Start the Nessus Service:

```text
sudo /etc/init.d/nessusd start
```

4. Open up Firefox and goto https://localhost:8834/. You may be prompted with a security risk alert. Click Advanced... -> Accept the Risk and Continue.
5. Select the option `Nessus Essentials`.
6. Click the Skip button and enter the activation code from the email from Nessus.
7. Fill out the `Username` and `Password` fields.
8. Nessus will now install the plugins required for it to function. Takes a long time. Get some tea.
9. Log in with the account credentials made earlier. 

You can have 16 different (IP) targets with this license.

## Configuration

Scans can be configured based on different scan and policy templates. These templates will determine the settings 
that will be found within the scan policy settings. These are the general settings that can be accessed:

* [Basic](https://docs.tenable.com/nessus/Content/BasicSettings.htm): Specify security-related and organizational 
aspects of a scan or policy. These aspects will include the name of the scan, the targets of the scan, whether it is 
scheduled and who has access to it.
* [Discovery ](https://docs.tenable.com/nessus/Content/DiscoverySettings.htm) is where the ports to be 
scanned and the methods to be used in the discovery are set.
* Assessment is where and how the type of vulnerability scan to do is set. Nessus will check susceptibility of 
Web applications to attacks and other systems to brute-force attacks as well. This setting has sections allowing 
customisation of general scans to Windows, SCADA, Web applications, and even brute-force checks.
* Report sets how scan reports are generated and the information that should be included within them.
* [Advanced](https://docs.tenable.com/nessus/Content/AdvancedSettings.htm) sets scan efficiency and the operations of 
the scan, and allows for enabling scan debugging.

## Troubleshooting

### Forgotten password

1. Navigate to: `cd /opt/nessus/sbin`
2. List users: `./nessuscli lsuser`
3. Reset the password for user `username`: `./nessuscli chpasswd username`

### API access is disabled

Nessus displays warning "Nessus has detected that API access on this scanner is disabled" during usage. To fix this 
issue, stop the Nessus service, reset the configuration, restart Nessus and register again using the activation code.

1. Stop the Nessus service: `service nessusd stop`
2. Reset the configuration: `/opt/nessus/sbin/nessuscli fix --reset`
3. Start the Nessus service: `/etc/init.d/nessusd start`
4. Register Nessus using the activation code: `/opt/nessus/sbin/nessuscli fetch --register xxxx-xxxx-xxxx-xxxx-xxxx`
5. Login to Nessus to update plugins.