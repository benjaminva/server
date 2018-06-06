## Server Account configuration

1.	Get and account to access the server from the teacher …. Me >D 
2.	Download putty or any SSH client
3.	Download turboVNC viewer (for visual interface) https://sourceforge.net/projects/turbovnc/ 
4.	Connect to the server via SSH at IP: 10.25.24.6
5.	Enable X11 forwarding (for visual interface)
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
11. verify your password
12. selection option no ‘n’
13. look at the number of the end of the line (in this case 1) and write it down, you will use it in the next steps 
``` 
blablbablablablablabalabblablablabal…/gpuserver:1.log
```
14.	open turboVNC and type in the server: IP: 10.25.24.6:<port number>, this number thats shows at the end of the line when you run vncserver and it will change each time you login example: 
```
10.25.24.6:1
```
15. type in your password
16. click on the default option (the one on the left marked in blue…ish)

That’s is you are finished configuring your account in the server!
  
You can use the [editor on GitHub](https://github.com/benjaminva/serversetup.io/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/benjaminva/serversetup.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
