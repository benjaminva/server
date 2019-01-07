## Server Account configuration
1.	Get and account to access the server 
2.	Download putty or any SSH client [PUTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
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
11.	verify your password
12.	selection option no ‘n’
13.	look at the number of the end of the line (in this case 1) and write it down, you will use it in the next steps 
``` 
blablbablablablablabalabblablablabal…/gpuserver:1.log
```
### In turboVNC
14	open turboVNC and type in the server: IP: 10.25.24.6:<port number>, this number thats shows at the end of the line when you run vncserver and it will change each time you login example: 
```
10.25.24.6:1
```
15.	type in your password
16.	click on the default option (the one on the left marked in blue…ish)

That’s is you are finished configuring your account in the server!


## Loggin to the server:

### Putty
1.	Connect using SSH/ (or putty connect)
2.	Launch vncserver in server. (remember to check the number at the end of the line)
``` vncserver ```
3. 	To kill your own sessions manualy first use ```vncserver -list``` to see your sessions ids and then use ```vncserver -kill :[number]``` to kill a specific session, for example:
``` 
	~$ vncserver -list
	X DISPLAY #     PROCESS ID
	:11             15940
	:27             9773
	:24             11071

	~$ vncserver -kill :11
```
### TurboVNC
3.	Launch TurboVNC in your computer.
4.	Use the number provided (use the number you checked in step 2).
5.	Work in the server ...
6.	When you finish working with the server, you MUST close the graphic interface, AND run kill_session.sh in your SSH session. If you do not do this the server will start accumulating open sessions (which will be linked to your account, which means I will hunt you down and hurt you…..r grade per each session left open… hurt, as in, real bad).

## Using C++ in the server:
1.	To run a program simply write the code in and save it as a .cpp extension (c plus plus file) or .h (header file).
2.	Depending on what libraries you include you will need to use different compilation commands.
To compile c++ (.cpp) programs and specify name: 
```	
g++ <file.cpp> -o <name of executable.out> 
``` 
example: 
```
g++ main.cpp -o hash
```
To compile a nameless c++ program (a.out will be created) use: 
```
g++ <file.cpp>
``` 
example: 
```
g++ main.cpp
```
To compile c++ (.cpp) program with libraries (.h), make sure the rest of the files are in the same folder (path) use: 
```	
g++ <lib1.h> <lib2.h> <file.cpp> -o <name of executable.out> 
``` 
example: 
```
g++ unit.h exception.h hash.h main.cpp -o hash
```
3.To run program use:
```
./<file.out> 
``` 
example: 
```
./a.out
```

## Using CUDA in the server:

1.	To run a program simply write the code in and save it as a .cu extension.
2.	Depending on what libraries you include you will need to use different compilation commands. Download this libraries to work with the class examples [C]
To compile CUDA (.cu) programs use: 
```	
nvcc <file.cu> 
```
To compile with opengl use: 
```
nvcc file.cu -lglut -lGLU -lGL 
```
To compile with opencv use: 
```
nvcc file.cu `pkg-config --cflags --libs opencv` 
```
To compile opencv + opengl use: 
```
nvcc file.cu -lglut -lGLU -lGL `pkg-config --cflags --libs opencv` 
```
3.Depending on what libraries you include you will need to use different execution commands.	
To run program without OpenCV or GPL use:
```
./<file.out> 
```
To run program with OpenCV or GPL use
```
vglrun <file.out>
```
	
## Moving files to the server:

1.	Download FileZila
2.	Create a conection 
```
	a.	Host 			10.25.24.6
	b.	Protocol	 	SFTP - SSH File Transfer Protocol
	c.	Logon 			Normal
	d.	Username 		<idnumber>
	e.	Pwd			*******
```
3.	Use GUI and arrows to move between server and local machine.

## Using cuda-memcheck:
linux:
```
    cuda-memcheck ./a.out
```
on windows:
```
    cuda-memcheck a.exe
```
## Using keras in server
1.	Check what GPU is free with
```
	nvidia-smi
```
2.	Add to the top of your keras scrip/program the following code:
```
	import tensorflow as tf
	import keras.backend.tensorflow_backend as KTF

	def get_session(gpu_fraction=0.3):
	  gpu_options = tf.GPUOptions(per_process_gpu_memory_fraction=gpu_fraction)
	  return tf.Session(config=tf.ConfigProto(gpu_options=gpu_options))

	# Call function to only use a small part of the GPU and leave space for others to run their projects
	KTF.set_session(get_session())
```
3. 	Always run your project using the (CUDA_VISIBLE_DEVICES) command. This command tells keras in which GPU to run. If you do not use this command  you will be blocking (and wasting) the second GPU. Choose either GPU 0 or 1 depending on what step 1 (nvidia-smi) showed.
```
	CUDA_VISIBLE_DEVICES=0 python programa.py
	or
	CUDA_VISIBLE_DEVICES=1 python programa.py
```
