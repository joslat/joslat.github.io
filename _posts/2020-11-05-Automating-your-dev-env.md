---
layout: post
title: Automating the dev environment set-up with Chocolatey & Boxstarter
subtitle: No hands involved (after it)...
image: /img/202011_chocoIcon.png
bigimg: /img/202011_chocoLogo.png
tags:
  - Development
  - Automation
  - Package
  - Version
  - Software 
published: true
date: '2020-11-05'
---
# Automating the dev environment set-up with Chocolatey & Boxstarter   
   
I recently joined Swiss Life as Software Architect and Developer Community Lead, and of course I got some brand new shiny laptops which had to set up... 
This time, instead of installing everything manually decided to give it a go to a colleague recommendation - Thanks Andrei! use Chocolatey to perform the installations.   
What's Chocolatey? A Windows-only package/software management solution, enabling version management, dependencies, order of installation and a powerful inventory management, between other features.   

I digged in a bit and found Boxstarter. Boxstarter builds on top of Chocolatey & provides a repeteable and really easy way to deploy Windows environment installations using Chocolatey packages, which is also reboot resilient, and enables unnatended installations that need "reboot and continue" for any installation that requires it.   
   

## Why?   
Well if you are a software engineer like me, you'll appreciate a predefined installation that you can review, and automate in a completely unnatended way. Also it is repeateable so you  can restore it at any moment. In addition, you can evolve it, manage versions over time in a controlled way... and that can be priceless..   

Of course this does not fit all as we all have different Os and different set of favourite tools (except for HotChocolate) but this pretends to provide enough flexibility so we all can benefit and  save time through avoiding unnecesary work, automating the tedious installation and setting-up, and also afterwards not remembering if we installed or not a concrete software, component or plugin or enabled a windows feature...   

So, once you have a installation script, you can evolve it over time... and is free of human-errors (except on the choice of applications)
Essentially, save Time, Complexity and reduce cost. But, mostly, time.   

More on this on [why Chocolatey](https://chocolatey.org/why-chocolatey) and [why BoxStarter](https://boxstarter.org/WhyBoxstarter).      
   
Official websites:  
- [Chocolatey official site](https://chocolatey.org/)  
- [BoxStarter](https://boxstarter.org/)  
   

## Let's get it done!   
1.  First things first - Install Chocolatey  
    - First, you need to install Chocolatey. You can do that by running the scripts [found here](https://chocolatey.org/install). After you do that, you can start using Chocolatey to install applications. If you have some trouble you can follow the [more detailed instructions here](https://chocolatey.org/docs/development-environment-setup).    
    - Once installed, we can check that it works by opening PowerShell and issuing a chocolatey command such as `choco install vlc`. Note we will need an elevated (aka admin enabled) powershell for this. This "semi-manual" installation will ask us if we wan to install the package, or if we allow to install all the packages, in the case it needs an additional package... this is a bit bothersome, but avoidable adding the `-y` in our command, so let's do that again. We type  `choco install vlc -y`.   
    - To update we should use upgrade instead of install, such as:  `choco upgrade vlc -y`

2.  Install BoxStarter. 
    After Chocolatey we can proceed to install BoxStarter, we can use PowerShell or choco for this as it makes it more simpler. Just type from an administrative commandline:  `cinst boxstarter`  (and add the -y if you don't want to be asked)
    Note: cinst is short for `chocolatey install`.  
   
3.  Create the script   
    Next we can create the Installation script, it is basically made of PowerShell with some Chocolatey commands.   
    We can create it as a single text file or any text based HTTP resource (like a Github Gist)[https://gist.github.com/].   
    It should look like:  

    ```
    Set-WindowsExplorerOptions -EnableShowHiddenFilesFoldersDrives -EnableShowProtectedOSFiles -EnableShowFileExtensions
    Enable-RemoteDesktop
    
    cinst fiddler4
    cinst git
    cinst vscode
    cinst sublimetext2
    

    cinst Microsoft-Hyper-V-All -source windowsFeatures
    ```

  In my case, I created the script with the purpose of having a developer box for .NET, azure and web development. For this I installed Visual Studio 2019. And added some of the  recommendations from Scott Hanselman "ultimate developer tools" and others blog posts.   

  The outcome is located in a [GitHub gist I created for this purpose](https://gist.github.com/joslat/4bc82c9da1d8d5a0054426612944414e) and it looks as follows:   
  ```

  Set-ExplorerOptions -showProtectedOSFiles -showFileExtensions
  Enable-RemoteDesktop

  # Some OS feature setup
  cinst Microsoft-Hyper-V-All -source windowsFeatures

  # Installing some cool software
  cinst visualstudio2019professional --package-parameters "--allWorkloads --includeRecommended --includeOptional --passive --locale en-US"
  cinst resharper
  cinst vscode
  cinst azure-cli
  cinst git
  cinst github
  cinst sql-server-management-studio
  cinst 7zip
  cinst notepadplusplus
  cinst sysinternals
  cinst powertoys
  cinst notepad2
  cinst spotify
  cinst adobereader
  cinst google-chrome-x64
  cinst brave
  cinst imageresizerapp
  cinst skype
  cinst f.lux 
  cinst sysinternals
  cinst obs-studio
  ```    

As a note, I configured all the packages for Visual Studio to be installed, as it is always faster to uninstall than to install, so later on I will uninstall the unneeded packages. As I intended to run this unnatended, it is way easier to uninstall them later on than to install.   
You can customize your script by searching the available packages at the [Official Chocolatey package search](https://chocolatey.org/packages)


4. Run the script  

   Once created and reviewed, we can go and execute it from an elevated (read, with Administrator permissions) command prompt. 

   Invoke the the `Install-BoxstarterPackage` command pointing to the gist created above. For this we will need the RAW link to the GIST script content. In our case it would look like:  `Install-BoxstarterPackage -PackageName https://gist.githubusercontent.com/joslat/4bc82c9da1d8d5a0054426612944414e/raw/c8456fc0c94a2cb8883fa3d3f5a1abb914d15d54/boxstarter_newdev_script.txt -DisableReboots`  

   Note that I used the `-DisableReboots`  option as it is stated on the BoxStarter example, but BoxStarter runs from an elevated prompt and can handle reboots and continue with the installation tasks completely unnatended..


5. And keep it up to date!
   As mentioned, Chocolatey manages versions and what better than a GUI to help us keep our software base updated.
   I particularly like ChocolateyGUI again, get it with `cinst chocolateygui` and it shows our installed packages and if they have updates available.
   And it also allows to export the list of installed packages, providing a valuable help to keep our "list of favorite tools" up to date and in order.

## Concluding
A nice recommendation from a now ex-colleague, turned out to be a valuable addition to my coding weapon array, which I am gladly sharing with you ;)
As a last recommendation, if I am motivating you to start using Chocolatey and/or BoxStarter, I'd be curious to see your scripts - if you don't mind sharing. 
Or if you were using it already, I am still curious :)

Have fun and enjoy the extra time that these two lovely tools do provide!



 

