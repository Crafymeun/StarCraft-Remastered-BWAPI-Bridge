Krasi0Bot™ and Krasi0BotLauncher™ EULA, privacy policy and readme.
==========================
Last updated on 2024-03-23. You must always refer to the latest version of this file which can be found at: https://goo.gl/aXGF7j
==========================
Note: Before using this software, you must first agree to the "EULA / ToS / Privacy Policy" section below and the contents of the file `license.txt` (called THE LICENSE from now on) (the latest version can always be found at https://goo.gl/9pGjAk )! By continuing to use this software (`krasi0Bot` and `krasi0BotLauncher`) and its supporting services, you agree that you have read the EULA, Terms Of Use and Privacy Policy and THE LICENSE and that your use is subject to them.
==========================

Instructions:
--------------------------
* Internet access is required for this software (krasi0Bot and krasi0BotLauncher) to work properly, because it's been designed to operate as SaaS. It is not a pure desktop application.
* Make sure you have StarCraft BroodWar v1.16.1 installed (StarCraft: Remastered is NOT supported at this time).
* LF: 3 is required for the bot to play at its maximum strength. See the next section for the tutorial on running a match.
* Only a few maps are officially supported. They can be found in the latest version of the archive `supportedMaps_vX.7z` which can be downloaded from https://goo.gl/4wwfA8 . Additionally, you have to extract the contents of the latest version of the archive `BWTA2_vX.7z` into `StarCraft\bwapi-data\BWTA2`.
* Network games with very high latency like those on ICCUP or BNET are *NOT* supported. In order to play over the internet, you could use Tunngle and create a LAN UDP game.
* If you are already surely winning a game against the bot and don't want to play the game to the very end, make sure you quit *FIRST* the Starcraft instance where the bot is running. If you quit from your side (the Starcraft instance you are using), BWAPI would report that as a victory for the bot and that would mess up the bot's opening learning algorithms. The bot will often sent "GG" and quit if it is absolutely sure that is losing the game.


Playing a Bo7+ (best of 7, 9, 11, etc.) human player VS AI match against the bot using LF 3.
--------------------------
Detailed tutorial using krasi0BotLauncher at: https://goo.gl/JLN8JY


Running bot VS bot games
--------------------------
You could use sc-docker (https://github.com/Games-and-Simulations/sc-docker)


Dependencies (automatically downloaded and installed if you use krasi0BotLauncher):
--------------------------
1) Dependencies (place each file in the corresponding location): https://goo.gl/Wdy3i3
2) (UPDATED!) Offline terrain analysis data for some popular maps (unarchive the files in bwapi-data\BWTA2): https://goo.gl/Pozk69
3) The supported maps pack which the above offline terrain analysis is for: https://goo.gl/my41bo (info about some of the maps: http://sscaitournament.com/index.php?action=maps)
4) Chaoslauncher with LAN latency plugin: https://goo.gl/tznWDx . The password for the archive is 1
5) 7z free file archiver for Windows. In case you don't have it already installed, it can be downloaded from: https://goo.gl/s6mwQg
6) If you still get errors about missing DLL files, please install all of the vc_redist versions from: https://goo.gl/jpys4D


Feedback and questions
--------------------------
Please email me at: krasi000@gmail.com or find me on SSCAIT's Discord at: https://discord.gg/DqvHsq9 (nickname krasi0)


License (THE LICENSE)
--------------------------
See license.txt in the same archive. Before using the software, you must also agree to the latest version of THE LICENSE which can always be found at https://goo.gl/9pGjAk


For Donations:
--------------------------
Bitcoin address: 18YJpFWa6Cvj3vrQgPvyAPWcgChJG2yc1e


FAQ:
--------------------------
Q: Is StarCraft®: Remastered supported?
A: Unfortunately, BWAPI doesn't yet support Starcraft: Remastered. It does NOT even support a Starcraft BroodWar version after v1.16.1.
    That's why the SSCAIT stream isn't running remastered yet :(
    The ball is now in Blizzard's field who have vowed to work on BWAPI support in the future. Stay tuned! :)

Q: How strong is the bot? Can it beat a pro-level human player like Flash?
A: Not yet! :) The current strength level of top bots is around D+ / C- ICCUP rank. Although, krasi0Bot can beat some amateur level players in a Bo9 match, StarCraft is a very complicated game and it is going to take years until the best AIs start to consistently beat top human players like Flash. But don't worry! I've been working on exactly that. :P

Q: So what's your final goal? To make your bot the best StarCraft BroodWar AI in the world?
A: Nope! You crazy or what??? As is the case with any other BW AI developer out there, my bot is more about <buzzword of the day, e.g. deep learning, MCTS, IoT, blockchain, Web 2.0, React.js, etc.> than actually making it the best bot at Starcraft. I mean, the latter would be a boring, trivial task after all. No idea who would even bother with that?! Anyway, if you accidentally see my bot losing any games, that's my excuse! /s

Q: When will the source code of the bot be released?
A: Likely never. I wrote some parts of the source code of the bot (and the in-house developed libraries that it depends on) during periods when I was being contractually employed by one software company or another. This means that I need an explicit legally binding permission for any public release of that source code. Besides, I still haven't gotten around to weighing the benefits of doing so. Some companies like Wolfram Alpha and Deepmind still prefer to keep the source code of their implementations closed. There must be a good reason behind that. In case that event ever happens, it will be announced. Until then, the source code will remain closed.

Q: Have you used / incorporated any source code from other StarCraft AIs (bots)?
A: No, not at all! Perhaps it's kinda of an ego thing in my case, but I try to make the bot the best one out there while implementing everything entirely on my own. There are a few bots on GitHub that are open source and whose licenses allow code reuse, but I still prefer to implement everything from scratch (except for: 1) terrain analysis - I still make use of a fork of a very old version of BWTA2 and 2) in my code, there are still remnants of BWSAL - a legacy framework on top of BWAPI). I don't even look at other bots' source code so that I don't get tempted to copy ideas or implementations. At the same time, I, of course, make use of some open source C++ libraries like Boost.

Q: Why does the bot suck so much when playing against an opponent who has picked Random at the start of a game?
A: Short answer: "hiding your race is OP".
    Long answer (Disclaimer: I've copied some statements from other bot authors): Random was banned in pro-level human play (tournaments) due to the lack of actual decisions you can reasonably make in the early game. Those first moments are crucial. Think of the differences between TvZ and TvP. One can open 14 Nexus, one can 4/5 pool you.
    Basically, you're left with no deep strategic choices but to pick Random (and use cheese) yourself in order to be able to equally counter all of the *potential* cheese that's likely coming at you in the following game. That's especially true on 3+ player maps.

Q: Why is the game speed so fast (200+ FPS) when I run the bot in single player mode (against the built-in Blizzard AI)?
A: By default, the bot runs as fast as possible (so that more games can be played in the same period of time).
    If you'd like to watch single player games on normal speed, in the file `bwapi-data\AI\krasi0_<currentVersion>\settings\commonConfig.json`, set "gameSpeed": -1,

Q: Is the AI ever going to support the other two races - Protoss and Zerg?
A: Unfortunately, BroodWar AI development is a very slow, difficult and time consuming process. I work full time and can only spend a part of my spare time on improving the AI (which is my hobby and also my passion).
    Still, I hope to be able to make a really good Zerg bot in 2018. Fingers crossed, I will manage to find the necessary time for that. :)

Q: Why can't I use cheat codes or chat with other online users while the bot is running?
A: Sending chat messages is controlled via the same BWAPI flag that prevents a human user to controll the bot's units.
    Messing up with the AI's units breaks its play so the flag has been turned off, which prevents using the chat functionality, too.

Q: Why does the bot now require Administrator rights (elevated privileges)?
A: After having wasted more than 30 minutes on a few occasions trying to remotely debug weird errors and permission issues on some users' Windows systems, I've decided that I have had enough.
    Admin privileges typically avoid such issues altogether. Besides, if you run Chaoslauncher or StarCraft as admin, the krasi0 bot executable needs to be running as admin in order to successfully connect, too.

Q: What is an easier way to download the latest version of the bot without the need of using the launcher?
A: http://krasi0bot.krasi0.com/downloadKrasi0BotLatestVersion.php Keep in mind that this URL may NOT always provide the latest version and may sometimes be left behind.

-----

Special thanks go to:
--------------------------
    All other bot developers that submit to https://sscaitournament.com/ for the awesome 24/7 competition.
    Some source code and ideas inspired by:
The bot Stardust (https://github.com/bmnielsen/Stardust)
The bot PurpleWave (https://github.com/dgant/PurpleWave)


EULA / Terms of Service (ToS) / Terms of Use / Privacy Policy:
--------------------------
    First, you must agree to THE LICENSE referred above.
    This software sends ingame related data over the Internet after each game. Use it at your own risk. Read below for more details.

    Most of the dynamic configuration, play style parameters and some custom logic have been moved from the engine instance (krasi0AIClient.exe) to a central server. At the start of each game, the most up to date parameters and configuration data are automatically downloaded by the bot from the central server.
    Once a game ends, the bot uploads the game result along with some in game statistics (such as what types of units the bot and the opponent have each made during the game, did the bot get rushed early in the game, etc.) back to the server.
    This process allows the AI to improve over time (using ML /machine learning/ similar to GAs /Genetic Algorithms/) by gathering data from all running bot instances and then performing offline analysis. The newly adjusted parameters are then downloaded from the central server by each bot instance during subsequent games and the bot should (at least in theory) play slightly better and adapt accordingly after each game.
    Internet connectivity is disabled for AIs during competitions such as SSCAIT, SAIL, AIIDE and CIG, etc. so in these cases, krasi0Bot uses manually uploaded (by me) configuration files to the read/ folder which contain a recent version of the learned parameters and the bot itself doesn't transmit anything to the central server.
    Please note that when you use the software locally, *NO* user sensitive data, personal data or personally identifiable information (PII) (such as names, addresses, passwords, personal files, IP addresses, game replay files, etc.) gets uploaded to or stored on the central server! Only game related data gets transmitted. The connection is encrypted. The collected (game training) data will not be shared, sold or rented to any third party. This software is run in compliance with General Data Protection Regulation (GDPR).
    This service actually collects less data than what other human players see when you play StarCraft with them online. As a result, you remain fully anonymous to the service. Your privacy is guaranteed.
    If in doubt, please scan the files from this archive with your A/V software or even better - run the bot on a separate PC, or in a VM or another type of sandboxed environment.

    In case you don't agree with the disclaimer (ToS) above, please delete all files from the archive and do NOT use this software / service! Thank you! ;)

Additional Links:
--------------------------
    Modified BWAPI source: https://github.com/adakitesystems/bwapi/commits/locked-mod
    New BWAPI bots ladder: http://sail.krasi0.com/
    [SSCAIT] Student StarCraft AI Tournament & Ladder: https://sscaitournament.com/

==========================
Starcraft and Starcraft: Broodwar are trademarks of Blizzard Entertainment.

==========================
Copyright © 2018+ Krasimir Krastev, all rights reserved.
