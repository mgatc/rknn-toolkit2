**Mùlù** [TOC] ## 1. Lián bǎn tiáoshì jiǎnjiè RKNN Toolkit2 de lián bǎn gōngnéng yībān xūyào gēngxīn bǎn duāndì rknn_server hé librknnrt.So/librknnmrt.So, bìngqiě shǒudòng qǐdòng rknn_server cáinéng zhèngcháng gōngzuò. Rknn_server: Shì yīgè yùnxíng zài bǎnzǐ shàng de hòutái dàilǐ fúwù, yòng yú jiēshōu PC tōngguò USB chuánshū guòlái de xiéyì, ránhòu zhíxíng bǎn duān runtime duìyìng de jiēkǒu, bìng fǎnhuí jiéguǒ gěi PC. - Librknnrt.So: Shì yīgè bǎn duāndì RKNPU Runtime kù (fēi RV1103/RV1106/RV1103B píngtái bù shìyòng). - Librknnmrt.So: Shì zhuānyòng yú RV1103/RV1106/RV1103B píngtái de RKNPU Runtime kù. Kāijī hòu tōngguò ps mìnglìng chákàn rknn_server jìnchéng shìfǒu yǐ cúnzài, rúguǒ yǐ cúnzài, zé bù xūyào shǒudòng qǐdòng, fǒuzé xūyào shǒudòng qǐdòng. ## 2. Huánjìng yāoqiú ### 2.1 Yìngjiàn huánjìng běn wéndàng shìyòng rúxià yìngjiàn píngtái: - RV1103 - RV1103B - RV1106 - RV1126B - RK3562 - RK3566 xìliè - RK3568 xìliè - RK3576 xìliè - RK3588 xìliè ### 2.2 Ruǎnjiàn huánjìng - ruò shǐyòng dòngtài xíngzhuàng shūrù RKNN móxíng, yāoqiú rknn_server hé RKNPU Runtime kù bǎnběn >=1.5.0. - Ruò shǐyòng dàyú 2GB de móxíng, yāoqiú rknn_server bǎnběn >=2.0.0B0. - Zài RV1103/RV1106/RV1103B děng xiǎo nèicún píngtái shàng, jiànyì rknn_server bǎnběn >=2.1.0. ## 3. Rknn_server cúnfàng mùlù rknn_server cúnfàng zài runtime mùlù xià, qǐng gēnjù bǎnzǐ shàng de xìtǒng xuǎnzé xiāngyìng bǎnběn de rknn_server, bùtóng xīnpiàn hé xìtǒng duìyìng de rknn_server lùjìng rúxià: ### 3.1 Android píngtái |xìtǒng |lùjìng | |-----|-----| |32-bit Android|runtime/Android/rknn_server/arm/rknn_server| |64-bit Android|runtime/Android/rknn_server/arm64/rknn_server| ### 3.2 Linux píngtái |xīnpiàn |xìtǒng |lùjìng | |-----|-----|-----| |RV1103/RV1106/RV1103B|32-bit Linux|runtime/Linux/rknn_server/armhf-uclibc/usr/bin/rknn_server| |qítā xīnpiàn |32-bit Linux|runtime/Linux/rknn_server/armhf/usr/bin/rknn_server| |qítā xīnpiàn |64-bit Linux|runtime/Linux/rknn_server/aarch64/usr/bin/rknn_server| ## 4. Qǐdòng bùzhòu ### 4.1 Android píngtái jìnrù rknpu2 gōngchéng de gēn mùlù, zài PC duān zhíxíng xiàliè mìnglìng qǐdòng dàilǐ fúwù: 1. Chóngxīn guà zài xìtǒng fēnqū, shǐ xìtǒng fēnqū chóngxīn kě xiě ``` adb root&& adb remount ``` 2. Gēngxīn dàilǐ chéngxù ``` // 64-bit Android xìtǒng adb push runtime/Android/rknn_server/arm64/rknn_server/vendor/bin/ // 32-bit Android xìtǒng adb push runtime/Android/rknn_server/arm/rknn_server/vendor/bin/ ``` 3. Gēngxīn RKNPU runtime kù ``` // 64-bit Android xìtǒng adb push runtime/Android/librknn_api/arm64-v8a/librknnrt.So/vendor/lib64 // 32-bit Android xìtǒng adb push runtime/Android/librknn_api/armeabi-v7a/librknnrt.So/vendor/lib ``` 4. Xiūgǎi dàilǐ chéngxù quánxiàn ``` adb shell chmod +x/vendor/bin/rknn_server ``` 5. Qǐdòng dàilǐ fúwù ``` adb shell"killall rknn_server" adb shell"nohup/vendor/bin/rknn_server >/dev/null"& ``` 6. Jiǎnchá dàilǐ fúwù shìfǒu qǐdòng chénggōng: ``` Adb shell ps -ef|grep rknn_server ``` chákàn shìfǒu yǒu `rknn_server`de jìnchéng id, rúguǒ cúnzài biǎoshì dàilǐ fúwù qǐdòng chénggōng; fǒuzé qǐng zài bǎnzǐ shàng shǒudòng qǐdòng dàilǐ fúwù, bùzhòu rúxià: Adb shell mìnglìng**jìnrù bǎnzǐ shell jièmiàn**hòu, zhíxíng xiàliè mìnglìng qǐdòng dàilǐ fúwù ``` nohup/vendor/bin/rknn_server >/dev/null& ``` ### 4.2 Linux píngtái (fēi RV1103/RV1106/RV1103B) 1. Gēngxīn dàilǐ chéngxù ``` // 64-bit Linux xìtǒng adb push runtime/Linux/rknn_server/aarch64/usr/bin/rknn_server/usr/bin/ // 32-bit Linux xìtǒng adb push runtime/Linux/rknn_server/armhf/usr/bin/rknn_server/usr/bin/ ``` 2. Gēngxīn RKNPU runtime kù ``` // 64-bit Linux xìtǒng adb push runtime/Linux/librknn_api/aarch64/librknnrt.So/usr/lib // 32-bit Linux xìtǒng adb push runtime/Linux/librknn_api/armhf/librknnrt.So/usr/lib ``` 3. Xiūgǎi dàilǐ chéngxù quánxiàn ``` adb shell chmod +x/usr/bin/rknn_server ``` 4. Qǐdòng dàilǐ fúwù ``` adb shell"killall rknn_server" adb shell"nohup/usr/bin/rknn_server >/dev/null"& ``` 5. Jiǎnchá dàilǐ fúwù shìfǒu qǐdòng chénggōng: ``` Adb shell ps -ef|grep rknn_server ``` chákàn shìfǒu yǒu `rknn_server`de jìnchéng id, rúguǒ cúnzài biǎoshì dàilǐ fúwù qǐdòng chénggōng; fǒuzé qǐng zài bǎnzǐ shàng shǒudòng qǐdòng dàilǐ fúwù, fāngfǎ rúxià: Adb shell mìnglìng**jìnrù bǎnzǐ shell jièmiàn**hòu, zhíxíng xiàliè mìnglìng qǐdòng dàilǐ fúwù ``` nohup/usr/bin/rknn_server >/dev/null& ``` ### 4.3Linux píngtái (RV1103/RV1106/RV1103B) RV1103/RV1106/RV1103B shàng shǐyòng de RKNPU Runtime kù shì librknnmrt.So, shǐyòng armhf-uclibc mùlù xià de rknn_server, qǐdòng bùzhòu rúxià: 1. Gēngxīn dàilǐ chéngxù ``` adb push runtime/Linux/rknn_server/armhf-uclibc/usr/bin/rknn_server/oem/usr/bin ``` 2. Gēngxīn RKNPU runtime kù ``` adb push runtime/Linux/librknn_api/armhf-uclibc/librknnmrt.So/oem/usr/lib ``` 3. Xiūgǎi dàilǐ chéngxù quánxiàn ``` adb shell chmod +x/oem/usr/bin/rknn_server ``` 4. Qǐdòng dàilǐ fúwù ``` adb shell"killall rknn_server" adb shell"nohup/oem/usr/bin/rknn_server >/dev/null"& ``` 5. Jiǎnchá dàilǐ fúwù shìfǒu qǐdòng chénggōng: ``` Adb shell ps |grep rknn_server ``` chákàn shìfǒu yǒu `rknn_server`de jìnchéng id, rúguǒ cúnzài biǎoshì dàilǐ fúwù qǐdòng chénggōng; fǒuzé qǐng zài bǎnzǐ shàng shǒudòng qǐdòng dàilǐ fúwù, fāngfǎ rúxià: Adb shell mìnglìng**jìnrù bǎnzǐ shell jièmiàn**hòu, zhíxíng xiàliè mìnglìng qǐdòng dàilǐ fúwù ``` nohup/oem/usr/bin/rknn_server >/dev/null& ``` ## 5. Chákàn rknn_server xiángxì rìzhì dàilǐ fúwù mòrèn bù kāiqǐ xiángxì rìzhì, rú yù dào lián bǎn guòchéng bàocuò, xū kāiqǐ xiángxì rìzhì lái dìngwèi cuòwù yuányīn, qǐng cānkǎo xiāngyìng píngtái zhíxíng bùzhòu: ### 5.1 Android píngtái 1. Shèzhì huánjìng biànliàng kāiqǐ xiángxì rìzhì, bìng qǐdòng dàilǐ: ``` Adb logcat -c adb shell"killall rknn_server" adb shell"setprop persist.Vendor.Rknn.Server.Log.Level 5&& nohup/vendor/bin/rknn_server >/dev/null"& ``` 2. Jiǎnchá dàilǐ fúwù shìfǒu qǐdòng chénggōng: ``` Adb shell ps -ef|grep rknn_server ``` 3. Yùnxíng PC shàng python tuīlǐ chéngxù 4. Chákàn yùnxíng rìzhì ``` adb logcat ``` 5. Kāiqǐ xiángxì rìzhì huì dǎozhì tuīlǐ sùdù biàn màn, huīfù mòrèn rìzhì děngjí de mìnglìng rúxià: ```Sh adb shell"killall rknn_server" adb shell"setprop persist.Vendor.Rknn.Server.Log.Level 0&& nohup/vendor/bin/rknn_server >/dev/null"& ``` ### 5.2 Linux píngtái (fēi RV1103/RV1106/RV1103B) 1. Chuàngjiàn mùlù, yòng yú bǎocún dàilǐ fúwù de xiángxì rìzhì ``` adb shell mkdir -p/userdata ``` 2. Shèzhì huánjìng biànliàng kāiqǐ xiángxì rìzhì, bìng qǐdòng dàilǐ: ``` Adb shell"killall rknn_server" adb shell"export RKNN_SERVER_LOGLEVEL=5&& nohup/usr/bin/rknn_server >/userdata/server.Log"& ``` 3. Jiǎnchá dàilǐ fúwù shìfǒu qǐdòng chénggōng: ``` Adb shell ps -ef|grep rknn_server ``` chákàn shìfǒu yǒu `rknn_server`de jìnchéng id, rúguǒ cúnzài biǎoshì dàilǐ fúwù qǐdòng chénggōng; fǒuzé qǐng zài bǎnzǐ shàng shǒudòng qǐdòng dàilǐ fúwù, fāngfǎ rúxià: Adb shell mìnglìng jìnrù bǎnzǐ shell jièmiàn hòu, zhíxíng xiàliè mìnglìng qǐdòng dàilǐ fúwù ``` export RKNN_SERVER_LOGLEVEL=5 nohup/usr/bin/rknn_server >/userdata/server.Log& exit ``` 4. Yùnxíng PC shàng python tuīlǐ chéngxù 5. Chákàn rìzhì ``` adb shell cat/userdata/server.Log ``` 6. Kāiqǐ xiángxì rìzhì huì dǎozhì tuīlǐ sùdù biàn màn, huīfù mòrèn rìzhì děngjí de mìnglìng rúxià: ```Sh adb shell"killall rknn_server" adb shell"export RKNN_SERVER_LOGLEVEL=0&& nohup/usr/bin/rknn_server >/userdata/server.Log"& ``` ### 5.3
Show more
5,000 / 5,000
**Table of Contents**

[TOC]

## 1. Introduction to board debugging
The board-to-board function of RKNN Toolkit2 generally requires updating the rknn_server and librknnrt.so/librknnmrt.so on the board side, and manually starting rknn_server to work properly.
rknn_server: is a background proxy service running on the board, which is used to receive the protocol transmitted from the PC via USB, then execute the corresponding interface of the board runtime, and return the result to the PC.

- librknnrt.so: is a board-side RKNPU Runtime library (not applicable to non-RV1103/RV1106/RV1103B platforms).
- librknnmrt.so: is a RKNPU Runtime library dedicated to the RV1103/RV1106/RV1103B platforms.

After booting up, use the ps command to check whether the rknn_server process already exists. If it already exists, it does not need to be started manually. Otherwise, it needs to be started manually.

## 2. Environment Requirements
### 2.1 Hardware Environment
This document applies to the following hardware platforms:

- RV1103
- RV1103B
- RV1106
- RV1126B
- RK3562
- RK3566 Series
- RK3568 Series
- RK3576 Series
- RK3588 Series

### 2.2 Software Environment
- If you use dynamic shape input RKNN model, rknn_server and RKNPU Runtime library version>=1.5.0 is required.
- If you use a model larger than 2GB, rknn_server version>=2.0.0b0 is required.
- On small memory platforms such as RV1103/RV1106/RV1103B, rknn_server version>=2.1.0 is recommended.

## 3. rknn_server storage directory
rknn_server is stored in the runtime directory. Please select the corresponding version of rknn_server according to the system on the board. The rknn_server paths corresponding to different chips and systems are as follows:
### 3.1 Android platform
|System|Path|
|-----|-----|
|32-bit Android|runtime/Android/rknn_server/arm/rknn_server|
|64-bit Android|runtime/Android/rknn_server/arm64/rknn_server|

### 3.2 Linux platform

|Chip|System|Path|
|-----|-----|-----|
|RV1103/RV1106/RV1103B|32-bit Linux|runtime/Linux/rknn_server/armhf-uclibc/usr/bin/rknn_server|
|Other chips|32-bit Linux|runtime/Linux/rknn_server/armhf/usr/bin/rknn_server|
|Other chips|64-bit Linux|runtime/Linux/rknn_server/aarch64/usr/bin/rknn_server|

## 4. Startup steps
### 4.1 Android platform
Enter the root directory of the rknpu2 project and execute the following command on the PC to start the proxy service:
1. Remount the system partition to make it writable again
```
adb root && adb remount
```
2. Update the proxy program
```
// 64-bit Android system
adb push runtime/Android/rknn_server/arm64/rknn_server /vendor/bin/
// 32-bit Android system
adb push runtime/Android/rknn_server/arm/rknn_server /vendor/bin/
```
3. Update the RKNPU runtime library
```
// 64-bit Android system
adb push runtime/Android/librknn_api/arm64-v8a/librknnrt.so /vendor/lib64
// 32-bit Android system
adb push runtime/Android/librknn_api/armeabi-v7a/librknnrt.so /vendor/lib
```
4. Modify the proxy program permissions
```
adb shell chmod +x /vendor/bin/rknn_server
```
5. Start the proxy service
```
adb shell "killall rknn_server"
adb shell "nohup /vendor/bin/rknn_server >/dev/null"&
```
6. Check whether the proxy service is started successfully:
```
adb shell ps -ef|grep rknn_server
```
Check whether there is a process id of `rknn_server`. If it exists, it means the proxy service is started successfully; otherwise, please manually start the proxy service on the board. The steps are as follows:
After entering the board shell interface through adb shell command**, execute the following command to start the proxy service

```
nohup /vendor/bin/rknn_server > /dev/null&
```

### 4.2 Linux platform (non-RV1103/RV1106/RV1103B)

1. Update the proxy program
```
// 64-bit Linux system
adb push runtime/Linux/rknn_server/aarch64/usr/bin/rknn_server /usr/bin/
// 32-bit Linux system
adb push runtime/Linux/rknn_server/armhf/usr/bin/rknn_server /usr/bin/
```
2. Update the RKNPU runtime library
```
// 64-bit Linux system
adb push runtime/Linux/librknn_api/aarch64/librknnrt.so /usr/lib
// 32-bit Linux system
adb push runtime/Linux/librknn_api/armhf/librknnrt.so /usr/lib
```
3. Modify the proxy program permissions
```
adb shell chmod +x /usr/bin/rknn_server
```
4. Start the proxy service
```
adb shell "killall rknn_server"
adb shell "nohup /usr/bin/rknn_server >/dev/null"&
```
5. Check whether the proxy service is started successfully:
```
adb shell ps -ef|grep rknn_server
```
Check whether there is a process id of `rknn_server`. If there is, it means that the proxy service is started successfully; otherwise, please manually start the proxy service on the board as follows:
adb After shell command **enter the board shell interface**, execute the following command to start the proxy service

```
nohup /usr/bin/rknn_server > /dev/null&
```

### 4.3 Linux platform (RV1103/RV1106/RV1103B)
The RKNPU Runtime library used on RV1103/RV1106/RV1103B is librknnmrt.so. Use rknn_server in the armhf-uclibc directory. The startup steps are as follows:
1. Update the proxy program
```
adb push runtime/Linux/rknn_server/armhf-uclibc/usr/bin/rknn_server /oem/usr/bin
```
2. Update the RKNPU runtime library
```
adb push runtime/Linux/librknn_api/armhf-uclibc/librknnmrt.so /oem/usr/lib
```
3. Modify the proxy program permissions
```
adb shell chmod +x /oem/usr/bin/rknn_server
```
4. Start the proxy service
```
adb shell "killall rknn_server"
adb shell "nohup /oem/usr/bin/rknn_server >/dev/null"&
```
5. Check whether the proxy service is started successfully:
```
adb shell ps |grep rknn_server
```
Check whether there is a process id of `rknn_server`. If there is, it means that the proxy service is started successfully; otherwise, please manually start the proxy service on the board as follows:
adb shell command **After entering the board shell interface**, execute the following command to start the proxy service

```
nohup /oem/usr/bin/rknn_server > /dev/null&
```

## 5. View rknn_server detailed log
By default, detailed log is not enabled for proxy service. If an error occurs during the board connection process, detailed log needs to be enabled to locate the cause of the error. Please refer to the steps for the corresponding platform:
### 5.1 Android platform
1. Set environment variables to enable detailed log and start the proxy:
```
adb logcat -c
adb shell "killall rknn_server"
adb shell "setprop persist.vendor.rknn.server.log.level 5 && nohup /vendor/bin/rknn_server >/dev/null"&
```
2. Check whether the proxy service is started successfully:

```
adb shell ps -ef|grep rknn_server
```
3. Run the python inference program on the PC
4. View the running log
```
adb logcat
```
5. Enabling detailed log will slow down the inference speed. The command to restore the default log level is as follows:

```sh
adb shell "killall rknn_server"
adb shell "setprop persist.vendor.rknn.server.log.level 0 && nohup /vendor/bin/rknn_server >/dev/null"&
```

### 5.2 Linux platform (not RV1103/RV1106/RV1103B)

1. Create a directory to save detailed logs of the proxy service
```
adb shell mkdir -p /userdata
```
2. Set environment variables to enable detailed logs and start the proxy:
```
adb shell "killall rknn_server"
adb shell "export RKNN_SERVER_LOGLEVEL=5 && nohup /usr/bin/rknn_server >/userdata/server.log"&
```
3. Check whether the proxy service is started successfully:
```
adb shell ps -ef|grep rknn_server
```
Check whether there is a process id of `rknn_server`. If there is, it means the proxy service has been started successfully; otherwise, please manually start the proxy service on the board as follows:
After entering the board shell interface with the adb shell command, execute the following command to start the proxy service
```
export RKNN_SERVER_LOGLEVEL=5
nohup /usr/bin/rknn_server >/userdata/server.log&
exit
```
4. Run the python inference program on the PC
5. View the log
```
adb shell cat /userdata/server.log
```

6. Enabling detailed logs will slow down the inference speed. The command to restore the default log level is as follows:

```sh
adb shell "killall rknn_server"
adb shell "export RKNN_SERVER_LOGLEVEL=0 && nohup /usr/bin/rknn_server >/userdata/server.log"&
```

### 5.3
Send feedback
5,000 character limit. Use the arrows to translate more.
Translation results available