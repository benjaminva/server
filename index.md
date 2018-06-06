## Server Account configuration

1.	Get and account to access the server from the teacher …. Me >D 
2.	Download putty or any SSH client
3.	Download turboVNC viewer (for visual interface) [Turbo](https://sourceforge.net/projects/turbovnc/) 
4.	Connect to the server via SSH at IP: 10.25.24.6
5.	Enable X11 forwarding (for visual interface)
### In the Server
6.	In the server create file kill_session.sh with nano
```
 nano kill_session.sh 
```
7.	Copy and paste the following line into the file and save the file:
```
kill `ps -f | awk '{if ($8 ~ /Xvnc/) print $2;}'`
```
8.	on the shell make the file executable
```
chmod +x kill_session.sh
```
9.	configure turboVNC server, on the server type
```
	vncserver
```
10.	type your password 
11.     verify your password
12.     selection option no ‘n’
13.     look at the number of the end of the line (in this case 1) and write it down, you will use it in the next steps 
``` 
blablbablablablablabalabblablablabal…/gpuserver:1.log
```
### In turboVNC
14.	open turboVNC and type in the server: IP: 10.25.24.6:<port number>, this number thats shows at the end of the line when you run vncserver and it will change each time you login example: 
```
10.25.24.6:1
```
15.      type in your password
16.      click on the default option (the one on the left marked in blue…ish)

That’s is you are finished configuring your account in the server!
