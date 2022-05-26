# How to connect this repo to your local obsidian 
## Windows
1. **Create a [Github](https://github.com) account, if you don't already have one.**

2. **Install [Git for Windows](https://git-scm.com/download/win)**
	- "When installing, make sure to enable the command line PATH, otherwise obsidian git has no means of accessing and automating the backup for you."(For more details: [source](https://github.com/gitobsidiantutorial/obsidian-git-tut-windows))

3. **Install [github desktop](https://desktop.github.com/) and log in to your github account (File > Options > Account).**

4. **Install the [github Command Line Interface](https://cli.github.com/)**
	- This can be done a variety of ways, below are the commands to do so using the [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html) package management and environment management system:
		```
		conda install gh --channel conda-forge
		```
		
5. **Store your login credentials with the github CLI by typing in the Command Prompt:**
	```
	gh auth login
	```
	- Then choose 'GitHub.com' > 'HTTPS' > 'Login with a web browser'

6. **In the github desktop app, press File > Clone Repository and paste this URL:**
	- https://github.com/LR-97/Pudendal_Vault.git
	- Clone the repository to your Desktop folder by editing the local path appropriately
7. **Download [Obsidian](https://obsidian.md/), if you haven't yet**
8. **In Obsidian, find the 'Open Another Vault' button on the bottom left portion of the screen. Select the 'Open Folder as Vault Option' and select the 'Pudendal_Vault' repository folder in your desktop**
	- The Pudendal_Vault folder folder should now be displayed in Obsidian, and you should be able to browse its contents. 
9. **Install the Obsidian Git plugin, and set hotkeys for Commit, Push, and Pull**
	- Disable safe mode in the community plugins tab if you haven't already. Browse the community plugins and search for `Obsidian Git`. Install and enable it.
	- Go to the 'Settings' tab, find 'Obsidian Git' under 'Community Plugins', and set hotkeys for the commit, push, and pull actions. 


## MAC OS:
- Create a [Github](https://github.com) account, if you don't already have one.
#incomplete 

## See Also:
- [[Managing Branches]]