CVE-2019-17671
CVE-2023-22809
 Done research on sudo 1.8.29 but other cves like cve-2021-3156 came up with details on privelege escalation from heap overflow. Tried to run the script by blasty, however GLIBC_2.34 version wasn't found, so it couldn't run. Other method to check was sudoedit -s /, no error was given.

Decided to lookup other exploits related to the kernel version as it's quite old (2021)

Came across CVE-2021-3560 which is an exploit using <a href="https://github.blog/2021-06-10-privilege-escalation-polkit-root-on-linux-with-bug/">polkit</a>, to confirm I wanted to know if it was running the version of polkit I was thinking of:

    rpm -q polkit

The version is 0.115, on the <a href="https://github.com/secnigma/CVE-2021-3560-Polkit-Privilege-Esclation">github page</a> also states that it was tested on 0.115. The exploit is timed-based attack, so running the script may take multiple tries according to the author.  

Details of the attack are triggered by starting a dbus-send and killing it while polkit is processing the request, more specifically the SetPassword D-bus method and creating a new user with sudo privs.

user secnigma was created, it's password is secnigmaftw

I decided to change the user and password to my credentials instead lol

My first 2 attempts failed, you also have to be really fast with switching to root or reading the flag since root is running a cleanup.sh script.

I'll leave this here, so you don't have to type it:

    sudo cat /root/root.txt