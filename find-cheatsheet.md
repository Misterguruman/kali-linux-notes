#LINUX COMMAND NOTES AND KALI "REMEMBER THESE" AREA
###Created: 3/14/2021
###Author : Joseph Langford

I'm trying to make this a git repository to share with others. Linking the markdown so I don't have to keep searching for it:
[GitHub Guide to Markdown](https://guides.github.com/features/mastering-markdown/)

# *FIND* command examples 

## *Man page description:* find - search for files in a directory hierarchy

##recusive list of all folders/files from cwd
	find . 

##search from cwd for something with a particular name
	find -name log

##search only for directories, and start from somewhere else
	find /home/ -type d -name log

##search only for files, and pipe errors to no-mans-land
	find / -type f -name evil 2> /dev/null

##search for a file that ENDS IN a string in thier name
	find /var -type f -name "*log" 2> /dev/null

##search for a file that CONTAINS A STRING in their name
	find / -type f -name "*log*" 2> /dev/null

##only return search items that were created x amount of days ago. Use minus because it's in the past. Postitive is the future
	find / -type f -name "*log*" -mtime -7 2> /dev/null

##execute a command on the results of your find. In this example we'll delete the files. THIS IS RISKY
	find /home/guru -type f -name "*log*" -exec rm {} ;

###Other noteable takeaways:
> When executing from the results of your search use ; to run the command on each result one at a time.
> use + to run the command on all of the results at once.
> essentiall you can run anything and {} will be replaced the results of find
> you can run multiple commands by stringing -execs together, see wrap up

#WRAP UP EXAMPLE: Take every htb notes file you've made in the last 30 days, copy them to a desktop folder and create one large file on your desktop to review
	find /home/mike/htb/boxes -type f -name "*notes*" -mtime -30 -exec cp {} /home/mike/Desktop/notes \; -exec cat {} >> /home/mike/Desktop/notes/masternotes.txt \;

#IMPORTANT: While these examples are using logs as an example. It's bad form to use this method to clear log files, see log rotate
#ALSO:      Don't use the -exec rm {} \; with sudo unless you are also comfortable driving with your eyes closed. It's just risky regardless
