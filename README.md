# WifiMapDrive
  If your windows machine uses WiFi and you would like to map network drives, e.g. for file shares, this will often fail because Windows' attempt to connect to the shared drive will happen before the WiFi connection has been fully established.
  
  This is a set of batch files that will put a time delay (2s by default) before attempting to connect to a share. This doesn't actually map the drive, but it makes the share available.

  The script runs per-user, not per-machine. So if you have multiple users you'll need to set it up multiple times. There is a group policy object for executing tasks when the machine boots up, but you run into similar problems. Besides, mapping a network drive is tied to a user account anyway.
  
  Using group policy, you could probably force every user on the domain to run this script anyway. Might make sense for an enterprise where most machines are using WiFi instead of Ethernet, or if ethernet negotiation takes too long (as mine does, since it goes over a couple of switches before hitting the router/DHCP).

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
  # Done.
  
##TODO##
- [ ] Investigate using Task Scheduler condition: "start only if the following network connection is available"
- [ ] Add command to actually map the shared drive, instead of net start.
- [ ] Orchestration to automatically install, including setting up task
- [ ] Hide command window when it launches so it doesn't intrude
  
