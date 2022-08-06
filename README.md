# HomeStoryCup XX - extension mod

A StarCraft II extension mod implementing WCS GameHeart with bug fixes and performance improvements.
Available on Americas, Europe and Korean servers.

![Find HomeStoryCup XX extension mod](https://pbs.twimg.com/media/FUlMat4WQAItXQm?format=jpg&name=medium)

### Observer UIs supporting this mod's features:

- [GameHeart 3.5](https://www.dropbox.com/s/egixonbgilk3no8/GameHeart_3.5.SC2Interface?dl=1)
- [Pro2020 AhliMod 1.1](https://www.dropbox.com/s/g47yvccechvmiqn/Pro2020ahliMod_1.1.SC2Interface?dl=1)

Editor to edit settings/hotkeys:
- [Settings Editor (Windows only)](https://www.dropbox.com/s/3f2a9ta6sbjzmrs/Observer%20UI%20Settings%20Editor%20Setup.exe?dl=1)

### All Changes compared to WCS GameHeart 1.25/Americas
- **Changes**
  - new feature: added new graphs:
    - Resources Lost differential graph on Hotkey Numpad3
    - Resources Gathered comparative graph on Hotkey Numpad4
  - new feature: player camera positions are now shown on minimap in 1vs1
  - new feature: neutral units are selectable through the fog
  - Workers Killed Notifications are now enabled when there are 2-4 players
  - Upgrade Notifications are enabled in games with 1-4 players
  - labels in Upgrade Notifications will resize to make their text fit
  - added production tab to leaderpanel that can be used to display chrono boost near the unit icon
  - moved default observed player from 14 to 15 (Hostile). This allows 14 player FFAs
  - Upgrade Notifications' icon can now be clicked to select the facility researching it
  - production tags and notifications now dynamically change to reflect alliance colors
  - added technical assistance for Observer Interfaces
    - saves the player slot number of each player to the PlayerId score
      - this assists observer interfaces in figuring out which Player Id is the left/right player in 1vs1 matches
    - saves the player status in the PlayerStatus score
      - this assists observer interfaces in figuring out if a player is still playing, left in victory/defeat/tie
    - animation event "TextUpdated" is fired when worker killed counter's text is updated => Observer UIs can animate
    - added player score that provides a player's starting position belonging to the initial 1=left or 2=right team for observer interfaces
- **Bug Fixes**
  - fixed Dark Shrine not showing upgrades in research on a tag
  - fixed potential bug when worker is killed at the same time as that player's notification timer expires resulting in a hidden notification and subsequently resulting in a wrong displayed count when the next one is killed
  - fixed not respecting facility slot limit which breaks the entire upgrade notification system, if upgrades in research exceed 100
  - fixed a bug when UI upgrade notification slots are exceeded (> 50) and the upgrade is cancelled/finished in that slot
  - fixed a Reactor being destroyed causing a blue unit icon when the player is supply blocked
  - fixed white production labels being able to appear briefly on screen at the map start
  - Worker Killed Notification counts larger than 99 will now shrink to fit instead of showing an ellipsis
  - fixed the last upgrade notification slot never being used
  - fixed having more than 50 upgrades causing further upgrades to not be displayed. Now the limit is 100 as previously intended
  - graph shortcuts are now disabled when not playing a 1vs1 instead of showing an empty graph dialog
- **SC2 Bug Fixes**
  - Units Lost Resources:
    - Overlords with Ventral Sacs and Overseers made from them will report its actual resource worth on death
      - this was 25/25 too low
    - Archons will report their actual resource worth on death instead of assuming the Archon was created by one HT and one DT
  - corrected score amount of Upgrades to match resource costs:
    - Cloaking Field, Hyperflight Rotors, Infernal Pre-Igniter, Drilling Claws, Smart Servos,
    - Tunneling Claws, Charge, Extended Thermal Lance, Flux Vanes
  - Observer Leaderpanel:
    - removed Reaper's KD8 Charges from the structures tab
    - fixed Reactors and Tech Labs creating multiple buttons
- **Optimizations**
  - fixed performance issues of Battlecruiser script triggers created by Blizzard
    - the game will now use less CPU when issuing commands and when units execute abilities (global improvement for all units)
    - the BC's behavior did not change
  - production label check filters missiles faster (trigger runs 30% faster on average)
  - optimized production label's UI code to use less resources and not save unused entries into the data table
    - this will make the script slow down less over time
  - improved upgrade notification update thread to not scan used slots multiple times
  - re-ordered unit type checks based on likelihood
  - reduced minimum loop iterations when updating upgrade notifications
  - trigger events are now only registered, if the feature is enabled and can function
  - remove some upgrade notification text styles from trigger script as it was set in UI already
  - production tags do not contain more slots than the unit require (e.g. Nexus has at most 1 production slot)
  - minor trigger action de-duplication
  - eliminated duplicated calculations
  - eliminated unnecessary variable allocations
  - eliminated duplicated function calls with additional variables
  - less code is executed for disabled features
  - removed superfluous upgrade name overrides
  - more general trigger optimizations based on the trigger debugger's execution duration
    - all failed conditions will now appear in failed executions instead of only the initial checks (triggers return 0)
