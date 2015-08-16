This document contains instructions on how to download Android BSPs for Intel Bay Trail-M/D and Bay Trail-I devices.  Please refer to the appropriate section depending on what hardware you have.  There are sections for:

• Intel Bay Trail-M/D Android 4.4.2 ww28 – now obsolete
• Intel Bay Trail-M/D Android 4.4.2 ww19 beta – now obsolete
• Intel Bay Trail-I Android 4.4.2 ww28 – now obsolete
• Intel Bay Trail-M/D Android 4.4.4 ww40
• Intel Bay Trail-I Android 4.4.4 ww41 – now obsolete
• Intel Bay Trail-M/D Android 5.0 ww47
• Intel Bay Trail-I Android 4.4.4 ww05

Please contact your local Wind River representative if you have any problems.




BYT-M/D v4.4.2 ww28 (obsolete): Instructions for downloading and using the Intel Android BSP for Bay Trail-M/D devices
This release is for Android v4.4.2 (known as Kit Kat).  Internally it is known as the ww28 phase 3 release, first available from Intel on July 11, 2014.  This release includes the full release for the Android Open Source Project (AOSP) and the appropriate Intel patches for that release.  It is meant for platforms which have the Intel Atom Bay Trail-M or Bay Trail-D processor.  This release will not work for devices with the Bay Trail-I or Bay Trail-T processor.

1. Make a new directory for your build and change directory into it:

$ cd
$ mkdir bytmd_442_ww28
$ cd bytmd_442_ww28

2. Download the file to your local Linux machine.  This is a huge 21.3 GB file.

ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww28.tar.gz

You can use your browser to download the files, or you can use the following script if you have wget installed:

wget ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww28.tar.gz

I *think* wget has an option to retry on failure, so you might want to enable that.

3. Download the bytmd_442_ww28.md5 file and use it to verify the integrity of the downloaded files.  The file is at:
ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww28.md5

Verify the downloaded files as follows:

$ md5sum -c bytmd_442_ww28.md5
bytmd_442_ww28: OK

4. Untar them into a working directory:

$ mkdir work
$ cd work
$ tar xfvz <path to>/bytmd_442_ww28.tar.gz

This creates a source tree from which you can now build your image.

5. This might no longer be required…  The one-time-setup script is available to help configure your host.  This script assumes you are using the recommended Ubuntu 10.04 LTS 64-bit release on your development host.  If you are using some other, unsupported Linux distro, you may need to adjust the script.  If you have already configured your system, then the script may not be necessary.  If necessary, run the script as follows:

$ sudo chmod 755 vendor/intel/support/one-time-setup
$ sudo ./vendor/intel/support/one-time-setup

Answer ‘yes’ to all the questions.

If the script fails, you may need to run some of the commands from the script manually.

6. The Sun Java™ Development Kit version 6 (jdk6) is required to build the software.  To see what version you have installed:

$ java –version

or

$ dpkg –list | grep –i jdk 

Steps for installing Sun Java6:

a. Download the Java SE 6 JDK from:  http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase6-419409.html  
b. Select the Linux x64 package (non-RPM) from the resulting page. 
c. Open a Terminal window 
d. Type ‘su’ to get root access (using your root password) 
e. Change to /usr/lib. (‘cd /usr /lib’) 
f. Create a jvm folder. (‘mkdir jvm’) 
g. Change to this folder (‘cd jvm’) and copy the jdk package you downloaded in step #2 to it. 
h. Change the permissions of the binary to a+x (‘chmod a+x jdk<TAB>’) 
i. Execute the binary (‘./jdk<TAB>’)
j. If necessary, verify your /usr/lib/jvm/java-6-sun symbolic link points to the new version of the jdk (‘sudo ln –sf /usr/lib/jvm/jdk1.6.0_45 /usr/lib/jvm/java-6-sun’) 

7. Compile the image:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-user

If you'd prefer to compile the userdebug variant, change this command too:

$ lunch byt_m_crb_64-userdebug
$ make publish_linux_tools
$ make flashfiles -j8

This assumes you have an 8 core system; adjust 8 as appropriate (NOTE: You can use the command ‘cat /proc/cpuinfo’ to see information about the processor on your system, or more specifically, ‘cat /proc/cpuinfo | grep ^processor | wc -l’ to see how many processors are available.)

At this point the image files for flashing will be created under:

bytmd_442_ww28/work/out/target/product/byt_m_crb/

The recommended image is live.img, which allows you to choose to run Android directly from the USB drive or to install Android on the local disk.  Other images may be present there, but are not recommended for use.

8. Now insert the USB drive into the Linux development system and discover its assigned path by using:

$ ls /dev/sd*

Alternatively, dmesg can be used:

$ dmesg

Find out which partition (sdb, sdc, etc.) that the USB drive is mounted too.  Now unmount all partitions on the USB drive.  Replace ‘sdb1’ below with the appropriate ‘sdx’ as found above.

$ umount /dev/sdb1
$ umount /dev/sdb2

Again, be sure to use the appropriate ‘sdx’ for your system!!!!  If you select the wrong “sdx”, you might reformat your hard drive.

Format the USB stick using a disk utility tool if required.  Write the image to the USB drive (again, assuming the USB drive has been assigned to sdb)

$ sudo dd if=out/target/product/byt_m_crb/live.img of=/dev/sdb

9. Plug the USB drive containing the live.img into one of the USB ports and boot the system.





BYT-M/D v4.4.2 ww19 (obsolete):  Instructions for downloading and using the Intel Android BSP for Bay Trail-M/D devices
This release is for Android v4.4.2 (known as Kit Kat).  Internally it is known as the ww19 beta release, first available from Intel on May 16, 2014.  This release includes the full release for the Android Open Source Project (AOSP) and the appropriate Intel patches for that release.  It is meant for platforms which have the Intel Atom Bay Trail-M or Bay Trail-D processor.  This release will not work for devices with the Bay Trail-I or Bay Trail-T processor.

1. Make a new directory for your build and change directory into it:

$ cd
$ mkdir bytmd_442_ww19
$ cd bytmd_442_ww19

2. Download the files to your local Linux machine.  These files are over 1 GB each and will take some time to download.  This particular release does not include repo or git history.

ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.00
ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.01
ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.02
ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.03
ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.04

You can use your browser to download the files, or you can use the following script if you have wget installed:

wget ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.00
wget ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.01
wget ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.02
wget ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.03
wget ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442_ww19.04

3. Download the bytmd_442.md5 file and use it to verify the integrity of the downloaded files.  The file is at:
ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_442.md5

Verify the downloaded files as follows:

$ md5sum -c bytmd_442.md5
bytmd_442_ww19.00: OK
bytmd_442_ww19.01: OK
bytmd_442_ww19.02: OK
bytmd_442_ww19.03: OK
bytmd_442_ww19.04: OK

4. Assemble the individual files and untar them into a working directory:

$ mkdir work
$ cd work
$ cat ../bytmd_442_ww19.0? | tar xfvj -

This creates a source tree from which you can now build your image.

5. The one-time-setup script is available to help configure your host.  This script assumes you are using the recommended Ubuntu 10.04 LTS 64-bit release on your development host.  If you are using some other, unsupported Linux distro, you may need to adjust the script.  If you have already configured your system, then the script may not be necessary.  If necessary, run the script as follows:

$ sudo chmod 755 vendor/intel/support/one-time-setup
$ sudo ./vendor/intel/support/one-time-setup

Answer ‘yes’ to all the questions.

If the script fails, you may need to run some of the commands from the script manually.

6. The Sun Java™ Development Kit version 6 (jdk6) is required to build the software.  To see what version you have installed:

$ java –version

or

$ dpkg –list | grep –i jdk 

Steps for installing Sun Java6:

a. Download the Java SE 6 JDK from:  http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase6-419409.html  
b. Select the Linux x64 package (non-RPM) from the resulting page. 
c. Open a Terminal window 
d. Type ‘su’ to get root access (using your root password) 
e. Change to /usr/lib. (‘cd /usr /lib’) 
f. Create a jvm folder. (‘mkdir jvm’) 
g. Change to this folder (‘cd jvm’) and copy the jdk package you downloaded in step #2 to it. 
h. Change the permissions of the binary to a+x (‘chmod a+x jdk<TAB>’) 
i. Execute the binary (‘./jdk<TAB>’)
j. If necessary, verify your /usr/lib/jvm/java-6-sun symbolic link points to the new version of the jdk (‘sudo ln –sf /usr/lib/jvm/jdk1.6.0_45 /usr/lib/jvm/java-6-sun’) 

7. Compile the image:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-user

If you'd prefer to compile the userdebug variant, change this command too:

$ lunch byt_m_crb_64-userdebug
$ make publish_linux_tools
$ make flashfiles -j8

This assumes you have an 8 core system; adjust 8 as appropriate (NOTE: You can use the command ‘cat /proc/cpuinfo’ to see information about the processor on your system, or more specifically, ‘cat /proc/cpuinfo | grep ^processor | wc -l’ to see how many processors are available.)

At this point the image files for flashing will be created under:

bytmd_442_ww19/work/out/target/product/byt_m_crb/

The recommended image is live.img, which allows you to choose to run Android directly from the USB drive or to install Android on the local disk.  Other images may be present there, but are not recommended for use.

8. Now insert the USB drive into the Linux development system and discover its assigned path by using:

$ ls /dev/sd*

Alternatively, dmesg can be used:

$ dmesg

Find out which partition (sdb, sdc, etc.) that the USB drive is mounted too.  Now unmount all partitions on the USB drive.  Replace ‘sdb1’ below with the appropriate ‘sdx’ as found above.

$ umount /dev/sdb1
$ umount /dev/sdb2

Again, be sure to use the appropriate ‘sdx’ for your system!!!!  If you select the wrong “sdx”, you might reformat your hard drive.

Format the USB stick using a disk utility tool if required.  Write the image to the USB drive (again, assuming the USB drive has been assigned to sdb)

$ sudo dd if=out/target/product/byt_m_crb/live.img of=/dev/sdb

9. Plug the USB drive containing the live.img into one of the USB ports and boot the system.





BYT-I v4.4.2 ww28 (obsolete):  Instructions for downloading and using the Intel Android BSP for Bay Trail-I devices
This release is for Android v4.4.2 (known as Kit Kat).  Internally it is known as the ww28 release, first available from Intel on July 11, 2014.  This release includes the full release for the Android Open Source Project (AOSP) and the appropriate Intel patches for that release.  It is meant for platforms which have the Intel Atom Bay Trail-I processor.  This release will not work for devices with the Bay Trail-M, -D or -T processor.  

The full release is 23.7 GB and is in one tarball.  This includes .git and .repo history.

If you’d just like to try an Android image on your Bay Trail I device, you can download the 300 MB “byti-live-user.img” and install it.  This is a pre-built binary image that is ready to load.  Jump to step #8 of the instructions and substitute in the appropriate image name.

1. Make a new directory for your build and change directory into it:

$ cd
$ mkdir byti_442_ww28
$ cd byti_442_ww28

2. Download the files to your local Linux machine.  This will take some time.  If the connection drops or hangs, simply restart it and it should resume where it left off.

ftp://ftp.windriver.com/public/IAS/android_442i/byti_442_ww28.tar.gz

You can use your browser to download the files, or you can use the following script if you have wget installed:

wget ftp://ftp.windriver.com/public/IAS/android_442i/byti_442_ww28.tar.gz

3. Download the byti_442_ww28.tar.md5 file and use it to verify the integrity of the downloaded files.  The file is at:

ftp://ftp.windriver.com/public/IAS/android_442i/byti_442_ww28.tar.md5

Verify the downloaded files as follows:

$ md5sum -c byti_442_ww28.tar.md5
byti_442_ww28.tar.gz: OK

4. Untar them into a working directory:

$ tar xzvf byti_442_ww28.tar.gz

This creates a source tree from which you can now build your image.

5. The one-time-setup script is available to help configure your host.  This script assumes you are using the recommended Ubuntu 10.04 LTS 64-bit release on your development host.  If you are using some other, unsupported Linux distro, you may need to adjust the script.  If you have already configured your system, then the script may not be necessary.  If necessary, run the script as follows:

$ sudo chmod 755 vendor/intel/support/one-time-setup
$ sudo ./vendor/intel/support/one-time-setup

Answer ‘yes’ to all the questions.

If the script fails, you may need to run some of the commands from the script manually.

6. The Sun Java™ Development Kit version 6 (jdk6) is required to build the software.  To see what version you have installed:

$ java –version

or

$ dpkg –list | grep –i jdk 

Steps for installing Sun Java6:

a. Download the Java SE 6 JDK from:  http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase6-419409.html  
b. Select the Linux x64 package (non-RPM) from the resulting page. 
c. Open a Terminal window 
d. Type ‘su’ to get root access (using your root password) 
e. Change to /usr/lib. (‘cd /usr /lib’) 
f. Create a jvm folder. (‘mkdir jvm’) 
g. Change to this folder (‘cd jvm’) and copy the jdk package you downloaded in step #2 to it. 
h. Change the permissions of the binary to a+x (‘chmod a+x jdk<TAB>’) 
i. Execute the binary (‘./jdk<TAB>’)
j. If necessary, verify your /usr/lib/jvm/java-6-sun symbolic link points to the new version of the jdk (‘sudo ln –sf /usr/lib/jvm/jdk1.6.0_45 /usr/lib/jvm/java-6-sun’) 

7. Compile the image:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-user  ?$ make flashfiles –j8

If you’d prefer to compile the userdebug variant, change these commands too:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-userdebug    
$ make flashfiles –j8

If you'd prefer to compile the engineering variant, change these commands too:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-eng      
$ make publish_linux_tools
$ make flashfiles -j8

This assumes you have an 8 core system; adjust 8 as appropriate (NOTE: You can use the command ‘cat /proc/cpuinfo’ to see information about the processor on your system, or more specifically, ‘cat /proc/cpuinfo | grep ^processor | wc -l’ to see how many processors are available.)

At this point the image files for flashing will be created under:

byti_442_ww28/out/target/product/byt_i_crb/

The above name needs to be confirmed.  Intel is now saying build output is at:
byti_442_ww28/pub/BYT_M_CRB_64/uefi-images/<variant>   (or is it byt_i_crb_64 ??)
where <variant> is eng, userdebug or user.

The recommended image is live.img, which allows you to choose to run Android directly from the USB drive or to install Android on the local disk.  Other images may be present there, but are not recommended for use.

8. Now insert the USB drive into the Linux development system and discover its assigned path by using:

$ ls /dev/sd*

Alternatively, dmesg can be used:

$ dmesg

Find out which partition (sdb, sdc, etc.) that the USB drive is mounted too.  Now unmount all partitions on the USB drive.  Replace ‘sdb1’ below with the appropriate ‘sdx’ as found above.

$ umount /dev/sdb1
$ umount /dev/sdb2

Again, be sure to use the appropriate ‘sdx’ for your system!!!!  If you select the wrong “sdx”, you might reformat your hard drive.

Format the USB stick using a disk utility tool if required.  Write the image to the USB drive (again, assuming the USB drive has been assigned to sdb)

$ sudo dd if=out/target/product/byt_i_crb/live.img of=/dev/sdb

9. Plug the USB drive containing the live.img into one of the USB ports and boot the system.





BYT-M/D v4.4.4 ww40:  Instructions for downloading and using the Intel Android BSP for Bay Trail-M/D devices
This release is for Android v4.4.4 (known as Kit Kat).  Internally it is known as the ww40 release, first available from Intel on Oct 6, 2014.  This release includes the full release for the Android Open Source Project (AOSP) and the appropriate Intel patches for that release.  It is meant for platforms which have the Intel Atom Bay Trail-M or Bay Trail-D processor.  This release will not work for devices with the Bay Trail-I or -T processor.  

The full release is ~20 GB and is in one tarball.  This includes .git and .repo history.

If you’d just like to try an Android image on your Bay Trail M/D device, you can download the 300 MB “bytmd_444_ww40.live.img” and install it.  This is a pre-built binary image that is ready to load.  Jump to step #8 of the instructions and substitute in the appropriate image name.

1. Make a new directory for your build and change directory into it:

$ cd
$ mkdir bytmd_444_ww40
$ cd bytmd_444_ww40

2. Download the files to your local Linux machine.  This will take some time.  If the connection drops or hangs, simply restart it and it should resume where it left off.

ftp://ftp.windriver.com/public/IAS/android_444md/bytmd_444_ww40.tar.gz

You can use your browser to download the files, or you can use the following script if you have wget installed:

wget ftp://ftp.windriver.com/public/IAS/android_444md/bytmd_444_ww40.tar.gz

3. Download the bytmd_444_ww40.tar.md5 file and use it to verify the integrity of the downloaded files.  The file is at:

ftp://ftp.windriver.com/public/IAS/android_442md/bytmd_444_ww40.tar.md5

Verify the downloaded files as follows:

$ md5sum -c bytmd_444_ww40.tar.md5
bytmd_444_ww40.tar.gz: OK

4. Untar them into a working directory:

$ tar xzvf bytmd_444_ww40.tar.gz

This creates a source tree from which you can now build your image.

5. The one-time-setup script is available to help configure your host.  This script assumes you are using the recommended Ubuntu 10.04 LTS 64-bit release on your development host.  If you are using some other, unsupported Linux distro, you may need to adjust the script.  If you have already configured your system, then the script may not be necessary.  If necessary, run the script as follows:

$ sudo chmod 755 vendor/intel/support/one-time-setup
$ sudo ./vendor/intel/support/one-time-setup

Answer ‘yes’ to all the questions.

If the script fails, you may need to run some of the commands from the script manually.

6. The Sun Java™ Development Kit version 6 (jdk6) is required to build the software.  To see what version you have installed:

$ java –version

or

$ dpkg –list | grep –i jdk 

Steps for installing Sun Java6:

a. Download the Java SE 6 JDK from:  http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase6-419409.html  
b. Select the Linux x64 package (non-RPM) from the resulting page. 
c. Open a Terminal window 
d. Type ‘su’ to get root access (using your root password) 
e. Change to /usr/lib. (‘cd /usr /lib’) 
f. Create a jvm folder. (‘mkdir jvm’) 
g. Change to this folder (‘cd jvm’) and copy the jdk package you downloaded in step #2 to it. 
h. Change the permissions of the binary to a+x (‘chmod a+x jdk<TAB>’) 
i. Execute the binary (‘./jdk<TAB>’)
j. If necessary, verify your /usr/lib/jvm/java-6-sun symbolic link points to the new version of the jdk (‘sudo ln –sf /usr/lib/jvm/jdk1.6.0_45 /usr/lib/jvm/java-6-sun’) 

7. Compile the image:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-user  ?$ make flashfiles –j8

If you’d prefer to compile the userdebug variant, change these commands too:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-userdebug    
$ make flashfiles –j8

If you'd prefer to compile the engineering variant, change these commands too:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-eng      
$ make publish_linux_tools
$ make flashfiles -j8

This assumes you have an 8 core system; adjust 8 as appropriate (NOTE: You can use the command ‘cat /proc/cpuinfo’ to see information about the processor on your system, or more specifically, ‘cat /proc/cpuinfo | grep ^processor | wc -l’ to see how many processors are available.)

At this point the image files for flashing will be created under:

bytmd_444_ww40/out/target/product/byt_i_crb/

The above name needs to be confirmed.  Intel is now saying build output is at:
bytmd_444_ww40/pub/BYT_M_CRB_64/uefi-images/<variant>   (or is it byt_i_crb_64 ??)
where <variant> is eng, userdebug or user.

The recommended image is live.img, which allows you to choose to run Android directly from the USB drive or to install Android on the local disk.  Other images may be present there, but are not recommended for use.

8. Now insert the USB drive into the Linux development system and discover its assigned path by using:

$ ls /dev/sd*

Alternatively, dmesg can be used:

$ dmesg

Find out which partition (sdb, sdc, etc.) that the USB drive is mounted too.  Now unmount all partitions on the USB drive.  Replace ‘sdb1’ below with the appropriate ‘sdx’ as found above.

$ umount /dev/sdb1
$ umount /dev/sdb2

Again, be sure to use the appropriate ‘sdx’ for your system!!!!  If you select the wrong “sdx”, you might reformat your hard drive.

Format the USB stick using a disk utility tool if required.  Write the image to the USB drive (again, assuming the USB drive has been assigned to sdb)

$ sudo dd if=out/target/product/byt_md_crb/live.img of=/dev/sdb

9. Plug the USB drive containing the live.img into one of the USB ports and boot the system.



BYT-I v4.4.4 ww41:  Instructions for downloading and using the Intel Android BSP for Bay Trail-I devices
This release is for Android v4.4.4 (known as Kit Kat).  Internally it is known as the ww41 release, first available from Intel on October 9, 2014.  This release includes the full release for the Android Open Source Project (AOSP) and the appropriate Intel patches for that release.  It is meant for platforms which have the Intel Atom Bay Trail-I processor.  This release will not work for devices with the Bay Trail-M, -D or -T processor.  

The full release is 21.6 GB and is in one tarball.  This includes .git and .repo history.

If you’d just like to try an Android image on your Bay Trail I device, you can download the 300 MB “byti_444_ww41.live.img” and install it.  This is a pre-built binary image that is ready to load.  Jump to step #8 of the instructions and substitute in the appropriate image name.

1. Make a new directory for your build and change directory into it:

$ cd
$ mkdir byti_444_ww41
$ cd byti_444_ww41

2. Download the files to your local Linux machine.  This will take some time.  If the connection drops or hangs, simply restart it and it should resume where it left off.

ftp://ftp.windriver.com/public/IAS/android_444i/byti_444_ww41.tar.gz

You can use your browser to download the files, or you can use the following script if you have wget installed:

wget ftp://ftp.windriver.com/public/IAS/android_444i/byti_444_ww41.tar.gz

3. Download the byti_444_ww41.tar.md5 file and use it to verify the integrity of the downloaded files.  The file is at:

ftp://ftp.windriver.com/public/IAS/android_444i/byti_444_ww41.tar.md5

Verify the downloaded files as follows:

$ md5sum -c byti_444_ww41.tar.md5
byti_444_ww41.tar.gz: OK

4. Untar them into a working directory:

$ tar xzvf byti_444_ww41.tar.gz

This creates a source tree from which you can now build your image.

5. The one-time-setup script is available to help configure your host.  This script assumes you are using the recommended Ubuntu 10.04 LTS 64-bit release on your development host.  If you are using some other, unsupported Linux distro, you may need to adjust the script.  If you have already configured your system, then the script may not be necessary.  If necessary, run the script as follows:

$ sudo chmod 755 vendor/intel/support/one-time-setup
$ sudo ./vendor/intel/support/one-time-setup

Answer ‘yes’ to all the questions.

If the script fails, you may need to run some of the commands from the script manually.

6. The Sun Java™ Development Kit version 6 (jdk6) is required to build the software.  To see what version you have installed:

$ java –version

or

$ dpkg –list | grep –i jdk 

Steps for installing Sun Java6:

a. Download the Java SE 6 JDK from:  http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase6-419409.html  
b. Select the Linux x64 package (non-RPM) from the resulting page. 
c. Open a Terminal window 
d. Type ‘su’ to get root access (using your root password) 
e. Change to /usr/lib. (‘cd /usr /lib’) 
f. Create a jvm folder. (‘mkdir jvm’) 
g. Change to this folder (‘cd jvm’) and copy the jdk package you downloaded in step #2 to it. 
h. Change the permissions of the binary to a+x (‘chmod a+x jdk<TAB>’) 
i. Execute the binary (‘./jdk<TAB>’)
j. If necessary, verify your /usr/lib/jvm/java-6-sun symbolic link points to the new version of the jdk (‘sudo ln –sf /usr/lib/jvm/jdk1.6.0_45 /usr/lib/jvm/java-6-sun’) 

7. Compile the image:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-user  ?$ make flashfiles –j8

If you’d prefer to compile the userdebug variant, change these commands too:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-userdebug    
$ make flashfiles –j8

If you'd prefer to compile the engineering variant, change these commands too:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-eng      
$ make publish_linux_tools
$ make flashfiles -j8

This assumes you have an 8 core system; adjust 8 as appropriate (NOTE: You can use the command ‘cat /proc/cpuinfo’ to see information about the processor on your system, or more specifically, ‘cat /proc/cpuinfo | grep ^processor | wc -l’ to see how many processors are available.)

At this point the image files for flashing will be created under:

byti_444_ww41/out/target/product/byt_i_crb/

The above name needs to be confirmed.  Intel is now saying build output is at:
byti_444_ww41/pub/BYT_M_CRB_64/uefi-images/<variant>   (or is it byt_i_crb_64 ??)
where <variant> is eng, userdebug or user.

The recommended image is live.img, which allows you to choose to run Android directly from the USB drive or to install Android on the local disk.  Other images may be present there, but are not recommended for use.

8. Now insert the USB drive into the Linux development system and discover its assigned path by using:

$ ls /dev/sd*

Alternatively, dmesg can be used:

$ dmesg

Find out which partition (sdb, sdc, etc.) that the USB drive is mounted too.  Now unmount all partitions on the USB drive.  Replace ‘sdb1’ below with the appropriate ‘sdx’ as found above.

$ umount /dev/sdb1
$ umount /dev/sdb2

Again, be sure to use the appropriate ‘sdx’ for your system!!!!  If you select the wrong “sdx”, you might reformat your hard drive.

Format the USB stick using a disk utility tool if required.  Write the image to the USB drive (again, assuming the USB drive has been assigned to sdb)

$ sudo dd if=out/target/product/byt_i_crb/live.img of=/dev/sdb

9. Plug the USB drive containing the live.img into one of the USB ports and boot the system.






BYT-M/D v5.0 ww47:  Instructions for downloading and using the Intel Android BSP for Bay Trail-M/D devices
This release is for Android v5.0 (known as Lollipop).  Internally it is known as the ww47 release, first available from Intel on December 5, 2015.  This release includes the full release for the Android Open Source Project (AOSP) and the appropriate Intel patches for that release.  It is meant for platforms which have the Intel Atom Bay Trail-M/D processor.  This release will not work for devices with the Bay Trail-I, or -T processor.  

The full release is 25.2 GB and is in one tarball.  This includes .git and .repo history.

1. Download the files to your local Linux machine.  This will take some time.  If the connection drops or hangs, simply restart it and it should resume where it left off.

ftp://ftp.windriver.com/public/IAS/android_50md/2014ww47_b_x64.tgz

You can use your browser to download the files, or you can use the following script if you have wget installed:

wget ftp://ftp.windriver.com/public/IAS/android_50md/2014ww47_b_x64.tgz

2. Download the 2014ww47_b_x64.tgz.md5 file and use it to verify the integrity of the downloaded files.  The file is at:

ftp://ftp.windriver.com/public/IAS/android_50md/2014ww47_b_x64.tgz.md5

Verify the downloaded files as follows:

$ md5sum -c 2014ww47_b_x64.tgz.md5
2014ww47_b_x64.tgz.gz: OK

4. Untar them into a working directory:

$ tar xzvf 2014ww47_b-x64.tgz

This creates a source tree from which you can now build your image.

5. The Java 7 is required for Android 5.0 Lollipop build, on Ubuntu, use OpenJDK 

• .	$ sudo apt-get update
• .	$ sudo apt-get install openjdk-7-jdk
• .	
• .	Add the following to the end of your ~/.bashrc: 
• .	    export JAVA_HOME=/opt/java/openjdk-7-java
• .	    export JAVA_FONTS=/usr/share/fonts/truetype
• .	    export ANT_HOME=/usr/share/ant
• .	    PATH=$JAVA_HOME/bin:$ANT_HOME/bin:$PATH
• .	    export CLASSPATH=.


6. Compile the image:

• 	Compile the user variant:
• 	$ source ./build/envsetup.sh
• 	$ lunch byt_m_crb64-user
• 	$ make -j8 publish_ci_bytm
• 			
• 	Compile the userdebug variant:
• 	$ source ./build/envsetup.sh 
• 	$ lunch byt_m_crb64-userdebug 
• 	$ make –j8 publish_ci_bytm 

This assumes you have an 8 core system; adjust 8 as appropriate (NOTE: You can use the command ‘cat /proc/cpuinfo’ to see information about the processor on your system, or more specifically, ‘cat /proc/cpuinfo | grep ^processor | wc -l’ to see how many processors are available.)

At this point the image files for flashing will be created under:

<build_dir>/out/target/product/byt_m_crb/


8. Flashing a device

1. 1.	First, insert the USB drive into the Linux development system and discover its assigned path by using 
$ ls /dev/sd*

Alternatively, dmesg can be used:

$ dmesg

Find out which partition (sdb, sdc, etc.) that the USB drive is mounted too.  Now unmount all partitions on the USB drive.  Replace ‘sdb1’ below with the appropriate ‘sdx’ as found above.

$ umount /dev/sdb1
$ umount /dev/sdb2

Again, be sure to use the appropriate ‘sdx’ for your system!!!!  If you select the wrong “sdx”, you might reformat your hard drive.

Format the USB stick using a disk utility tool if required.  Write the USB-Fastboot image to the USB drive (again, assuming the USB drive has been assigned to sdb)

$ sudo dd if=out/target/product/byt_m_crb/fastboot-usb.img  of=/dev/sdb


Plug the USB to target device & reboot the target device to EFI Internal Shell
• Press F2 -> Boot Manager -> EFI Internal Shell 
• fs<n>:
• LockDown.efi - If the keys are already inserted you will see the message "Platform is not in Setup Mode, cannot install Keys" so continue to next step 
Plug the USB to target device & reboot the target device to Fastboot mode
• Press F2 -> Boot Manager -> EFI USB Device -> Fastboot Mode
Note down the IP address that appears in the device screen or the terminal
Extract the .tgz image , and flash the image by running the interactive script - follow the instructions that appear when you run the script
• ./flash-all.sh -t <IP_ADDRESS_IN_THE_DEVICE_SCREEN>































BYT-I v4.4.4 2015ww05:  Instructions for downloading and using the Intel Android BSP for Bay Trail-I devices
This release is for Android v4.4.4 (known as Kit Kat).  Internally it is known as the 2015ww05 release, first available from Intel on January 21, 2015.  This release includes the full release for the Android Open Source Project (AOSP) and the appropriate Intel patches for that release.  It is meant for platforms which have the Intel Atom Bay Trail-I processor.  This release will not work for devices with the Bay Trail-M, -D or -T processor.  

The full release is 28.3 GB and is in one tarball.  This includes .git and .repo history.

If you’d just like to try an Android image on your Bay Trail I device, you can download the 300 MB “byti_444_2015ww05.live.img” and install it.  This is a pre-built binary image that is ready to load.  Jump to step #8 of the instructions and substitute in the appropriate image name.


1. Download the files to your local Linux machine.  This will take some time.  If the connection drops or hangs, simply restart it and it should resume where it left off.

ftp://ftp.windriver.com/public/IAS/android_444i/byti_444_2015ww05.tgz

You can use your browser to download the files, or you can use the following script if you have wget installed:

wget ftp://ftp.windriver.com/public/IAS/android_444i/byti_444_2015ww05.tgz

2. Download the byti_444_2015ww05.tgz.md5 file and use it to verify the integrity of the downloaded files.  The file is at:

ftp://ftp.windriver.com/public/IAS/android_444i/byti_444_2015ww05.tgz.md5

Verify the downloaded files as follows:

$ md5sum -c byti_444_2015ww05.tgz.md5
byti_444_2015ww05.tgz: OK

4. Untar them into a working directory:

$ tar xzvf byti_444_2015ww05.tar.gz
$ cd byti_444_2015ww05

This creates a source tree from which you can now build your image.


5. The Sun Java™ Development Kit version 6 (jdk6) is required to build the software.  To see what version you have installed:

$ java –version

or

$ dpkg –list | grep –i jdk 

Steps for installing Sun Java6:

a. Download the Java SE 6 JDK from:  http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase6-419409.html  
b. Select the Linux x64 package (non-RPM) from the resulting page. 
c. Open a Terminal window 
d. Type ‘su’ to get root access (using your root password) 
e. Change to /usr/lib. (‘cd /usr /lib’) 
f. Create a jvm folder. (‘mkdir jvm’) 
g. Change to this folder (‘cd jvm’) and copy the jdk package you downloaded in step #2 to it. 
h. Change the permissions of the binary to a+x (‘chmod a+x jdk<TAB>’) 
i. Execute the binary (‘./jdk<TAB>’)
j. If necessary, verify your /usr/lib/jvm/java-6-sun symbolic link points to the new version of the jdk (‘sudo ln –sf /usr/lib/jvm/jdk1.6.0_45 /usr/lib/jvm/java-6-sun’) 

6. Compile the image:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-user  ?$ make flashfiles –j8

If you’d prefer to compile the userdebug variant, change these commands too:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-userdebug    
$ make flashfiles –j8

If you'd prefer to compile the engineering variant, change these commands too:

$ source ./build/envsetup.sh
$ lunch byt_m_crb_64-eng      
$ make publish_linux_tools
$ make flashfiles -j8

This assumes you have an 8 core system; adjust 8 as appropriate (NOTE: You can use the command ‘cat /proc/cpuinfo’ to see information about the processor on your system, or more specifically, ‘cat /proc/cpuinfo | grep ^processor | wc -l’ to see how many processors are available.)

At this point the image files for flashing will be created under:

byti_444_2015ww05/out/target/product/byt_m_crb/

The above name needs to be confirmed.  Intel is now saying build output is at:
byti_444_2015ww05/pub/BYT_M_CRB_64/uefi-images/<variant>  
where <variant> is eng, userdebug or user.

The recommended image is live.img, which allows you to choose to run Android directly from the USB drive or to install Android on the local disk.  Other images may be present there, but are not recommended for use.

8. Now insert the USB drive into the Linux development system and discover its assigned path by using:

$ ls /dev/sd*

Alternatively, dmesg can be used:

$ dmesg

Find out which partition (sdb, sdc, etc.) that the USB drive is mounted too.  Now unmount all partitions on the USB drive.  Replace ‘sdb1’ below with the appropriate ‘sdx’ as found above.

$ umount /dev/sdb1
$ umount /dev/sdb2

Again, be sure to use the appropriate ‘sdx’ for your system!!!!  If you select the wrong “sdx”, you might reformat your hard drive.

Format the USB stick using a disk utility tool if required.  Write the image to the USB drive (again, assuming the USB drive has been assigned to sdb)

$ sudo dd if=./pub/BYT_M_CRB_64/uefi- images/<variant> /live.img of=/dev/sdb

9. Plug the USB drive containing the live.img into one of the USB ports and boot the system.
