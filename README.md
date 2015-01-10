# WifiMapDrive
  If your windows machine uses WiFi (or your ethernet connection takes too long, maybe because it has to go through a series of switches) and you would like to map network drives, e.g. for file shares, this will often fail because Windows' attempt to connect to the shared drive will happen before the connection has been fully established.
  
  If you map a drive, and configure a scheduled task in a particular way to run this batch script (it just calls net use), you'll get connected to your share (which should match what you mapped), although you'll still get a little error popup that says 'unable to connect to share'.

  The script runs per-user, not per-machine. So if you have multiple users you'll need to set it up multiple times. There is a group policy object for executing tasks when the machine boots up, but you run into similar problems. Besides, mapping a network drive is tied to a user account anyway.
  
  Using group policy, you could probably force every user on the domain to run this script with the same constraints anyway. Might make sense for an enterprise where most machines are using WiFi ior have slow ethernet connectivity establishment.

  To set up, do the following (in Windows 7, similar for 8):
  # Start > Control Panel > System and Security > Administrative Tools (near the bottom).
  ## If you're using 'large icons', just go to Administrative Tools.
  # In the left pane, right click on Task Scheduler Library and click Create Task
  # Name: Shared drive (or whatevery ou like)
  # Click the Triggers tab and click New...
  # Begin the task: > At log on
  # Run as specific user, and set the user to your account.
  # Click on Actions tab and click New...
  # Set the program/script to the mount-helper.bat file.
  # Set the "start in" to the same directory that the mount-helper.bat file is located in. Click Ok.
  # Click the Conditions tab and uncheck everything.
  # Check "Start only if the following network connection is available:
  ## You can choose the particular network required. Generally this will just be the one named 'Network' but you can double check in Adapter Settings.
  # Click OK
  # Done.
  
##TODO##
- [x] Investigate using Task Scheduler condition: "start only if the following network connection is available"
- [ ] Orchestration to automatically install, including setting up task and mapping drive
- [ ] Install prompts for list of connections to map and drive letters
  
