 
# Catalina, zsh, bash and conda environments

 I upgraded my operating system to *Mac OS Catalina* recently and found myself having to deal with strange python behaviour. One important change on Catalina vs Mojave is that the default terminal shell (=command interpreter) is now zsh and not bash anymore.  So if you had python installed on Mojave or earlier versions tailored to bash, these are the adjustments you need to do:


1. Get Oh-my-zh
2. Configure ~.zsh_profile 
3. Configure Catalina and conda environments
 
 
Why did they change to ZSH in the first place?  Well, because it exhibits improvements and higher flexibility over bash. The name 'zsh' is derived from the name of Yale professor **Zong Shao**. Some improvements over bash include themes and plugins, automatic cd, recursive path expansion, spelling correction, approximate completion, plugin and theme support. You can find more infos on zsh [here](https://www.google.com/url?q=https%3A%2F%2Fwww.howtoforge.com%2Ftutorial%2Fhow-to-setup-zsh-and-oh-my-zsh-on-linux%2F&sa=D&sntz=1&usg=AFQjCNGBErYlUA7rscNCs_p-J6DGRsX1yA). 


## 1.Get Oh-my-zh
### First step: Install homebrew (if not done already)
Homebrew is a useful tool to install  software on macOS operating systems and Linux with the command line. Another way of saying that it's ' a package management system'. For example in python, the package management systems are a) anaconda and b) pip, and for LaTeX, the package manger is  tlmgr. 

For *homebrew* you need to

```
a) install Xcode via Mac App Store

b) install command line tools (130MB)  with xcode-select --install

c) install Homebrew with :

/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
### Second step: Configure ZSH and get Oh-my-zsh

Oh-my-zsh is an open source framework for managing ZSH.  
Do you have zsh already?

```echo $SHELL```

**If yes**, install Oh-my-zh by typing 

```
	brew install wget

	wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh
```
 
Oh-my-zsh is installed in the **home directory '~/.oh-my-zsh'**

Next, create a new configuration for zsh. As with the bash shell, which has a configuration named '.bashrc', for zsh, we need a ``.zshrc`` configuration file. It's available in the oh-my-zsh templates directory.


Copy the template ``.zshrc.zsh-template`` configuration file to the home directory ``.zshrc`` and apply the configuration by running the source command:

```
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

source ~/.zshrc

cd ~/.oh-my-zsh/themes/

ls -a

vim ~/.zshrc
```
and then change the theme you want, e.g. ``ZSH_THEME='risto'``


### We need to configure the .zshr  for python

**Which python is in your PATH?** (Or which exectuable is triggered when typing ``python``)


`` which python ``

**MODIFY PATH**
`` export PATH="the-directory-with/anaconda3/bin:$PATH"``

However, we are not done yet. What would happen now is that every time I started a new terminal session, I needed to adjust my PATH variable. Annoying! I found the solution on [overflow](https://stackoverflow.com/conda-not-found-after-upgrading-to-macos-catalina):


<div style="padding: 15px; border: 1px solid transparent; border-color: transparent; margin-bottom: 20px; border-radius: 4px; color: #31708f; background-color: #d9edf7; border-color: #bce8f1;">
	<div class="linelist">
    <ul> You can find the entire anaconda3 environment in a shortcut link named 'Relocated Items' on your desktop. It appears as though the upgrade to Catalina does not allow the Conda environment to be installed under a user directory now likely having to do with the new system volume move to a read-only partition.
This issue has been opened as far back as June 10th, I am a little disappointed that it was not resolved before the Catalina upgrade came around.
There is a solution that appears to work without losing your environment, see this <a href="https://github.com/ContinuumIO/anaconda-issues/issues/10998#issuecomment-539215005">link</a>:
        <li> (optional) Copy the folder anaconda3   located in Relocated Items to /Users/myname/</li>
        <li><b>Open Terminal </b>   </li>
        <li> <b>Enter: export PATH='/Users/myname/anaconda3/bin:$PATH' </b>  </li>
        <li> <b>	Enter: conda init zsh  </li></b>
    </ul>
</div>
</div>

 


