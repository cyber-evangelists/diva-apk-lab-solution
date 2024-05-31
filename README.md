Here's a guide to get started with solving the challenges in DIVA, including the prerequisites mentioned:

### Prerequisites
Before you dive into solving challenges with DIVA, ensure you have the following tools installed and ready:

1. **Genymotion**: A fast and easy-to-use Android emulator used to run the DIVA app in a controlled environment. It's preferred for its performance and extensive device emulation capabilities.

2. **APKTool**: A tool for reverse engineering Android apk files. It allows you to decode resources to nearly original form and rebuild them after making modifications.

3. **JD-GUI**: A standalone graphical utility that displays Java source codes of “.class” files. You'll use it to inspect the decompiled source code of DIVA.

4. **Dex2Jar**: Tools to work with android .dex and Java .class files. Dex2Jar allows you to convert DIVA's dex files into jar files for easier analysis with JD-GUI.

5. **DIVA APK**: The Damn Insecure and Vulnerable App itself. Make sure to download it from a reliable source.

### Getting Started
Once you have all the prerequisites, follow these steps to start solving challenges:

1. **Set Up Your Environment**:
   - Install Genymotion and create a virtual device that matches the Android version DIVA supports.
   - Install APKTool, JD-GUI, and Dex2Jar on your machine.

2. **Install DIVA**:
   - Drag and drop the DIVA apk file into your Genymotion virtual device to install it, or use ADB (Android Debug Bridge) to install it with the command: `adb install path_to_diva_apk`.

3. **Familiarize Yourself With the Challenges**:
   - Open DIVA on your virtual device. Explore the app to understand the types of challenges it offers.

### Solving Challenges
To solve a challenge, you might need to reverse-engineer the app, inspect its code, modify its behavior, or exploit its vulnerabilities. Here's a general approach:

1. **Analyze the APK**:
   - Use APKTool to decompile the app and inspect its resources and manifest. This can reveal a lot about the app's structure and potential vulnerabilities.
   - Command: `apktool d diva.apk`

2. **Convert and Inspect Code**:
   - Use Dex2Jar to convert the APK's dex files into a Java jar file.
   - Command: `d2j-dex2jar classes.dex`
   - Then, use JD-GUI to open the jar file and inspect the decompiled source code for vulnerabilities.

3. **Solve Challenges**:
   - Each challenge will require a unique approach. For example, you might need to:
     - Modify the app's code or resources to bypass security checks.
     - Inject SQL commands to exploit SQL injection vulnerabilities.
     - Use debugging tools to understand how the app processes data and where it's vulnerable.

4. **Test Your Solutions**:
   - After modifying the app or preparing an attack, test it on the virtual device to see if your solution works.
   - Use Genymotion and ADB to debug and monitor the app's behavior during your tests.

### Tips for Success
- **Keep Learning**: The field of mobile security is vast. Use resources like security blogs, forums, and guides to learn new techniques and stay updated on vulnerabilities.
- **Practice Ethically**: Only use DIVA and other similar tools in a controlled, legal environment. Never exploit real apps without permission.
- **Collaborate**: Joining a community of like-minded individuals can accelerate your learning. Share your successes and learn from others' experiences.

Solving challenges in DIVA is a hands-on way to improve your understanding of mobile vulnerabilities and how to exploit them. As you progress, you'll develop a deeper understanding of Android security mechanisms and how to protect against common vulnerabilities.

#

### Vulnerabilities:
1. Insecure Logging
                        
2. Hardcoding Issues – Part 1

3. Insecure Data Storage – Part 1

4. Insecure Data Storage – Part 2

5. Insecure Data Storage – Part 3

6. Insecure Data Storage – Part 4

7. Input Validation Issues – Part 1

8. Input Validation Issues – Part 2

9. Access Control Issues – Part 1

10. Access Control Issues – Part 2

11. Access Control Issues – Part 3

12. Hardcoding Issues – Part2

13. Input Validation Issues – Part 

#
## Setting up Arsenal:

### Genymotion:

    https://www.genymotion.com/product-desktop/download/

you can download it from above link.

install android emulator in genymotion and setup emulator to proxy through the burp suite, you can take help from [here](https://www.youtube.com/watch?v=aqqdy7460yo)

### apktool:
    apt install apktool



### jd-gui:
    apt install jd-gui


### DIVA Apk:
    http://www.payatu.com/wp-content/uploads/2016/01/diva-beta.tar.gz

download it from above link

use below command to install apk into emulator.

    adb shell install <apk-name>

*adb can be found in ```Genymotion/Tools``` directory*

#
### Setting up analysis environment:

1. After download apk, extract it using normal extracting methods and rename it to ```diva-beta1```

2. Use apktool to decompile apk
    
    ``` apktool d <apk> ```

3. Now move to ```diva-beta``` directory  and open ```AndroidManifest.xml```.

4. Now move to ```diva-beta1``` directory and run below command in this directory.

    ```d2j-dex2jar classes.dex```

5. Open ```classes-dex2jar.jar``` file located within this directory.

    ```jd-gui classes-dex2jar.jar```


**Congratulations** you setup lab environment, now proceed to exploitation section.

#
## Exploitation:

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/0.png)



1. Insecure Logging:
   
enter any number in input filed  and click on `checkout`

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/1.png)


check logs using below command and replace "123456" with your input, you will see your input reflected in logs


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/1.1.png)



2. Hardcoding Issues – Part 1

this is hardcoding challenge this mean the Vendor Key is hardcoded in the application. In order to get the hardcoded key we need to do Reverse Engineering of this application.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/2.png)


so go to your jd-gui screen and you will see harcoreded credentials here.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/2.1.png)


3. Insecure Data Storage – Part 1:

Enter your creds in input fileds.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/3.png)



review the source code of this activity. We can see that credentials are stored in Shared Preferences.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/3.1.png)



Now go to this folder and you will see credentials.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/3.2.png)


4. Insecure Data Storage – Part 2:

This is similar challenge to previous one but credentials are stored in different location.


Enter your creds in input fileds.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/4.png)


This time credentials were stored in database ids2 and in its myuser table


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/4.1.png)




Goto to database folder in /data/data and you will see your credentials.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/4.2.png)



5. Insecure Data Storage – Part 3:

Enter the credentials from application.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/5.png)






The credentials were stored in temporary file


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/5.1.png)








Let’s access those temporary file from shell.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/5.2.png)









6. Insecure Data Storage – Part 4:

Enter the credentials from application.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/6.png)



The app is storing credentials in external storage.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/6.1.png)



We got the location, now access them from shell.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/6.2.png)



7. Input Validation Issues – Part 1:

 Now try to enter admin in input field, you will get details about admin user.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/7.png) 
 
 
 Hmmm, it is looking fetching data from database, let's try sql injection




![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/7.1.png)



sql injection was successful, we got all users detail.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/7.2.png)



8. Input Validation Issues – Part 2:
   

In this challenge we have to access local files using URL,

Let’s try to get file info from local storage other then valid url.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/8.png)


**Note:** the file you are trying to read will also exist in /sdcard, if not create one for pratice.
 

9. Access Control Issues – Part 1:


Accessing credentials from “View API Credentials” Button is completely legal. There is no issue in it. We need to check that can we directly access credentials without going through this activity or this checkpoint.




![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/9.png)



we look into "AndroidManifest.xml" for any exported android component, if any component is exported then it can be accessible outside the app.


we got one activity exported in "AndroidManifest.xml"


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/9.1.png)



Lets open the activity outside the app context.
We can see activity launched with sensitive activity without directly interacting with app.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/9.2.png)



10. Access Control Issues – Part 2:

This is same as above Vulnerablebut there is a slight twist.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/10.png)



We see into "AndroidManifest.xml" again and found another exported activity.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/10.1.png)



Now try to start this activity.



![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/10.2.png)


Oh no its asking for pin, we have to bypass this pin to access sensitive activity.




Now look into decompiled code using jd-gui, we can see that we have to provide some string and boolean value, 
but which is.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/10.3.png)





We see `APICreds2Activity` (which is much silialr as intent defined in `AndroidManifest.xml`) in decompiled code, now look into it, we get bool value we have need to change it from `false` to `true`, but we still need some string parameter.

we got some number in `getString()` function.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/10.4.png)



There is references in android in R.class, we check this for any reference related to above got number, yaa hooo, we got string which we can used as a paramter to access our secret activity.



![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/10.5.png)




Now its time to open the activity, Now arrange all got info into one command to get access.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/10.6.png)




11. Access Control Issues – Part 3:

Now again come to `AndoirdManifest.xml` and this time we see another component exported and which is `provider` component, this components manages access to data. 




![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/11.png)



Now check decompiled code for this `notesprovider`. 

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/11.1.png)


We got content provider uri in decompiled code.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/11.2.png)



Now lets try to acees it otside the app.



![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/11.3.png)



12. Hardcoding Issues – Part2:


We have to find vendor pin in order to access it,

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/12.png)



We can see its accesing `Divajni` class, click on it.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/12.1.png)




We can see in this code that , it is accessing divajni library.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/12.2.png)




Now goto `diva-lab1/lib/<anyfolder>` and you will got `libdivajni.so` file.




![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/12.3.png)




Now string to it and you got some string different then others, this string is a key to success.


![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/12.4.png)



Input htis key into the app.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/12.5.png)




13. Input Validation Issues – Part 3:

We have to crash this app by Dosing it,

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/13.png)




NOw generate 60 characters and add into the input filed and click on button.

![DIVA](https://github.com/cyber-evangelists/diva-apk-lab-solution/blob/main/screenshots/13.1.png)


