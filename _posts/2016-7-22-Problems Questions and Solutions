I start this post in the idea of collecting and centralizing technical problems and questions that I have through my work and study. It is a place to revisit if similar problem re-occurs or some knowledge fades away. I will keep adding new things into here, as well as collect the scattered notes of the past. 

# Keep SSH Sessions running after disconnection, and resume it later
from http://unix.stackexchange.com/questions/479/keep-ssh-sessions-running-after-disconnection?newreg=54f0dfa60fde4ed7881d617ab7a8a447
* Use nohup to make your process ignore the hangup signal:

	$ nohup long-running-process &
	$ exit

* You want to be using GNU Screen. It is super awesome!

	ssh me@myserver.com
	screen               #start a screen session
	run-a-long-process
	
CTRL+a , d to detatch from your screen session

	exit                 #disconnect from the server, while run-a-long-process continues
When you come back to your laptop:

	ssh me@myserver.com
	screen -r            #resume the screen session
Then check out the progress of your long-running process!

screen is a very comprehensive tool, and can do a lot more than what I've described. While in a screen session, try ctrl+a,? to learn a few common commands. Probably the most common are:

CTRL+a , c to create a new window
CTRL+a , n to switch to the next window in your screen session
CTRL+a , p to switch to the previous window in your screen session
if you log in from a bunch of different systems, you may have accidentally left yourself attached to an active screen session on a different computer. for that reason, I always resume with screen -d -r to ensure that if another shell is attached to my screen session, it will be detached before I resume it on my current system.

Other valuable answers:
http://unix.stackexchange.com/questions/89483/keeping-a-process-running-after-putty-or-terminal-has-been-closed
Screen Manual is here: https://www.gnu.org/software/screen/manual/screen.html