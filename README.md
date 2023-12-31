<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/invatorzen/PSDKPlugins">
    <img src="https://i.imgur.com/Q3LOc4v.png" alt="Logo" width="240" height="240">
  </a>

  <h3 align="center">Invatorzen's PSDKPlugins</h3>

  <p align="center">
    When I'm not gaming, working on my own project (Umbra) or working on mods, I like to make plugins. <br />
    So here they are. :D
    <br /> <br />
    <a href="https://reliccastle.com/members/781/#resources"><strong>You can find these on RelicCastle as well »</strong></a>
    <br />
    <br />
    <a href="https://github.com/invatorzen/InvatorzenPSDKPlugins/issues">Report Bugs</a>
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Jump to a plugin:</summary>
  <ul>
    <li><a href="#freeze-to-frostbite">Freeze to Frostbite</a></li>
    <li><a href="#non-binary-support">Non-Binary Support</a></li>
    <li><a href="#auto-run">Toggle Autorun</a></li>
    <li><a href="#daynightbgm">DayNightBGM Changer</a></li>
    <li><a href="#substitubes-balls">Substitube's Balls</a></li>
    <li><a href="#gen-9-consumables">Gen 9 Consumable Held Item Mechanics</a></li>
  </ul>
</details>

<!-- ABOUT THE PROJECT -->
## Quick intro
Hi! I'm Invatorzen, I've been working on Pokémon fan games since I was a kid but more seriously since I was in high-school. Starting with ROM Hacks and quickly getting overwhelmed as a kid I learned about 
fan games and heard about a kit called Pokémon Essentials. After working on my own project for a few years, I decided to start a new group project which is known as [Pokémon Umbra](https://twitter.com/PokemonUmbra). 
After another few years we decided to move to a newer kit called PSDK, which I have grown to learn and love and now make plugins for!
<br/><br/>
I'm very much an amateur dev, but I do enjoy making my own game and making these plugins in my free-time. I'm open to suggestions, but may never get to it if it's too demanding, out of my scope, or if I would never use it in my project.

<!-- Installing PSDK Plugins -->
## Installing PSDK Plugins
Installing PSDK plugins is made to be as easy as possible for users and is basically a drag and drop process.
<ol>
  <li>Download the psdkplug file you want directly from the repo or you can grab them all and download them as a zip.</li>
  <li>Drag the psdkplug files you want into your scripts folder.</li>
  <li>Run your project and the plugin manager will handle the rest!</li>
</ol>
<br/>
If any of the plugins have more instructions, it'd be indicated in their section.

<!-- Frostbite -->
## Freeze to Frostbite
This plugin requires an extra step:
<ul>
  <li>Make sure to make a backup or delete your "statusen.png" file so it replaces the frozen icon!</li>
</ul>

This plugin adds in a new status that's basically burn but reduces your special damage dealt. It procs guts, and can be prevented by magma armor. By default hail will make you 3x more likely to inflict frostbite, 
and frostbite does 1/8th the users MAX HP as damage per turn. (This is how burn works in PSDK.)

If you want to change the damage dealt or the effect, make a monkey patch. Something like:
```rb
module Battle
  module Effects
    class Status
      class Frostbite < Status
        private
        def frostbite_effect
          return (target.max_hp / 16).clamp(1, Float::INFINITY) # Change this
        end
      end
    end
  end
end
```
And you're good to go! To test if the status is working, give your first mon frostbite by typing ``$actors[0].status_frostbite`` and going into battle by typing ``S.MI.call_battle_wild(:bulbasaur, 5)`` in the cmd prompts.

<!-- Nb Support -->
## Non-Binary Support
This plugin does not require any extra steps to install, however do pay attention to the <a href="#proper-setup">proper setup!</a>

This plugin modifies how gender is handled in PSDK, which originally was using a switch. It is set through variable 495!
By default I believe each value represents:
<ol>
  <li>0 = Female</li>
  <li>1 = Male</li>
  <li>2 = Non-binary</li>
</ol>

If you'd like to change the variable, it's rather easy, make a monkey patch like:
```rb
module Yuki
  module Var
    GenderVar = 495 # Change this 
  end
end
```

### Proper Setup
<ul>
  <li>Overworld Sprites are set up just like before!</li>
  For example: gp.set_appearance_set('hero_01_cindy') with variable 495 = 1 would load the graphic "hero_01_cindy_f_walk"
  <li>Region map icons are simple!</li>
  Save an image in your graphics/interface/worldmap folder with the same name used for your character's overworld sprite!
  For example: "hero_01_white_f_walking" would be "hero_01_white_1" in the worldmap folder.
  <li>Setting up the bag is easy!</li>
  Just add another graphic to graphics/interface/bag called "bag_nb"!
</ul>
This is one of my first plugins, let me know if you find any bugs!

<!-- Auto-Run -->
## Auto-Run
This plugin requires extra steps:
<ul>
  <li>Open your "Data\configs\game_options_config.json" and add "toggled_running_choice" to the list of options.</li>
  <li>Go to Data/Text/Dialogs and open 100042.csv, line 11 represents "on" and 12 "off".</li>
  <li>Line 68 is the name/title of the option, 69 is the description!</li>
</ul>

This plugin will check if you have the switch that allows you to run enabled (basically checking if you have running shoes), if it is then it checks your option setting to see if you've enabled auto-run. You could modify this to activate on a switch if you wanted to and know what you're doing. 

<!-- DayNightBGM -->
## DayNightBGM

<!-- Sub's balls -->
## Substitube's Balls

<!-- Consumables -->
## Gen 9 Consumables
