##  DEPLOYMENT STEPS OF [PINT!](https://www.peopleintegrator.com/)

-Open Terminal(Git-bash)

PINT username
```
ssh pint@peopleintegrator.com 
```
PINT password
```
pint123! 
```
Now you're inside the Terminal
 
- Build project from the vscode terminal 

```
mvn clean install
```
```
mvn clean package
```

- Copy the WAR file from the "target" folder of your project and paste it into the "Downloads" folder.

- Delete old pint.war from server home:
```
rm -rf pint.war
```
- Check and confirm if it is deleted
```
ls -lrt
```
- Copy war to servers home directory: 
```
scp ~/Downloads/pint.war pint@peopleintegrator.com:/home/pint
```
 
- Copy war to PINT_WARFILES and change name to ROOT.war: 
```
sudo cp /home/pint/pint.war /home/pint/PINT_WARFILES/ROOT.war
```

## **- Tomcat steps**

- stopping the Tomcat 9 service using the "sudo" (superuser) privilege
```
sudo service tomcat9 stop
```
- Change the current Directory
```
cd /var/lib/tomcat9/webapps/
```
-  remove (delete) the file named "ROOT.war" and "ROOT" with superuser privileges.
```
sudo rm ROOT.war
```
```
sudo rm -rf ROOT
```
- copy the file "ROOT.war" from the source directory "/home/pint/PINT_WARFILES/" to the destination directory "/var/lib/tomcat9/webapps/" with superuser privileges.
```
sudo cp -i /home/pint/PINT_WARFILES/ROOT.war /var/lib/tomcat9/webapps/
```
-  start the Tomcat 9 service with superuser privileges
```
sudo service tomcat9 start
```
 
- optional step:
```
sudo service tomcat9 restart
```
Then You can refresh the link [PINT](https://www.peopleintegrator.com/).
