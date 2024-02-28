
# DIVA Solution:

DIVA(Damn Insecure and Vulnerable Application) is intentionaly insecure lab to practice android aap flaws, This is an interesting lab, we look how to solve the challenges.

## Prerequisites:
- **genymotion**
- **apktool**
- **jd-gui**
- **dex2jar** 
- **diva apk**

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




check logs using below command and replace "12345" with your input, you will see your input reflected in logs


2. 2. Hardcoding Issues – Part 1

this is hardcoding challenge this mean the Vendor Key is hardcoded in the application. In order to get the hardcoded key we need to do Reverse Engineering of this application.



so go to your jd-gui screen and you will see harcoreded credentials here.


3. Insecure Data Storage – Part 1:

Enter your creds in input fileds.





review the source code of this activity. We can see that credentials are stored in Shared Preferences.





Now go to this folde and you will see credentials.



4. Insecure Data Storage – Part 2:

This is similar challenge to previous one but credentials are stored in different location.





Enter your creds in input fileds.





This time credentials were stored in database ids2 and in its myuser table







Goto to database folder in /data/data and you will see your credentials.








5. Insecure Data Storage – Part 3:

Enter the credentials from application.









The credentials were stored in temporary file











Let’s access those temporary file from shell.












6. Insecure Data Storage – Part 4:

Enter the credentials from application.











The app is storing credentials in external storage.













We got the location, now access them from shell














7. Input Validation Issues – Part 1:

 Now try to enter admin in input field, you will get details about admin user.

 
 
 
 Hmmm, it is looking fetching data from database, let's try sql injection








sql injection was successful, we got all users detail.

8. Input Validation Issues – Part 2:

In this challenge we have to access local files using URL

Let’s try to get file info from local storage other then valid url.











9. Access Control Issues – Part 1:


Accessing credentials from “View API Credentials” Button is completely legal. There is no issue in it. We need to check that can we directly access credentials without going through this activity or this checkpoint.












we look into "AndroidManifest.xml" for any exported android component, if any component is exported then it can be accessible outside the app.

we got one activity exported in "AndroidManifest.xml"













Lets open the activity outside the app context.
We can see activity launched with sensitive activity with directly interacting with app.














10. Access Control Issues – Part 2:

This is same as above Vulnerablebut there is a slight twist.









We see into "AndroidManifest.xml" again and found another exported activity.










Now try to start this activity.










Oh no its asking for pin, we have to bypass this pin to access sensitive activity.












Now look into decompiled code using jd-gui, we can see that we have to provide some string and boolean value, but whic is.












We see `APICreds2Activity` (which is much silialr as intent defined in `AndroidManifest.xml`) in decompiled code, now look into it, we get bool value we have need to change it from `false` to `true`, but we still need some string parameter.

we got some number in `getString()` function.















There is references in android in R.class, we check this for any reference related to above got number, yaa hooo, we got string which we can used as a paramter to access our secret activity.

















Now its time to open the activity, Now arrange all got info into one command to get success.














11. Access Control Issues – Part 3:

Now again come to `AndoirdManifest.xml` and this time we see another component exported and which is `provider` component, this components manages access to data. 


















Now check decompiled code for this `notesprovider`. We got content provider uri in decompiled code.


















Now lets try to acees it otside the app.

















12. Hardcoding Issues – Part2:


We have to find vendor pin in order to access it, look into the decompiled code, we can see its accesing `Divajni` class, click on it.











We can see in this code that , it is accessing divajni library.














Now goto `diva-lab1/lib/<anyfolder>` and you will got `libdivajni.so` file.





















Now string to it and you got some string different then others, this string is a key to success.
















Input htis key into the app.















13. Input Validation Issues – Part 3:

We have to crash this app by Dosing it,





















NOw generate 60 characters and add into the input filed and click on button.
































































