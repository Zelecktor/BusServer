# BusServer

This Repository is made for use in Linux environment to connect multiple openkore instances.


## Quick Sart

* 1 Download the repository:
```
git clone https://github.com/PipeDeveloper/BusServer.git
```

* 2 Enter to the folder
```
cd BusServer
```

* 3 You may want to run it on a separate screen, for this download screen, then use the following commands:
```
sudo apt-get install screen

screen bash
```

* 4 Build and run bus-server.pl
```
perl bus-server.pl
```

* 5 Exit screen and let running bus server in background.
For this press `CTRL+A` release and then press `D`

  - If you want to enter again to the background console just re-attach screen for oppen the it again.
```
screen -list

screen -r <pit number>
```
Example:
```
screen -r 644
```

## Manually Loaded Bus Server

Command Line Switches
Command line switches can be detailed by loading the **Bus Server** perl script with the `--help` switch.

**`--bind=<host>`**

Specify a particular hostname or IP address the bus will listen on. This is equivalent to bus_server_host in sys.txt

Examples:
if you are running at localhost
```
--bind=192.168.1.10
--bind=10.0.0.10
```

If you are running on a server (multiples machines around the world) or at home (don't forget open your ports), use your public IP.
```
--bind=201.293.28.76
```

**`--help`**

Displays help for all switches.

**`--port=<portnumber>`**

Start the server at the specified port. Leave empty to use the first available port. Otherwise, acceptable port range is 1..65535.
 
**`--quiet`**

Supresses status messages.


A working example:
```
sudo perl bus-server.pl --bind=171.153.78.16 --port=10000
```


# Openkore Instances

To connect your openkore instance to the bus server, enter to **control** folder and open **sys.txt**

* 1 Search and change `bus 0` to `bus 1`

* 2 Add connection address

```
bus_server_host <host>
bus_server_port <port>
bus_userAgent
```

Following the example above

```
bus_server_host 171.153.78.16
bus_server_port 10000
bus_userAgent
```

You are done!


# Bus Plugins Set Up

* 1 Get your plugins on your openkore folder at **plugings/needs-review** and select your plugin, just drag it to the main folder.

`plugins/yourpluging.pl`

* 2 To add bus pluging to your openkore, enter to **control** folder and open **sys.txt**

Look for your pluging settings
  - The faster way is to change `loadPlugins 2` to `loadPlugins 1`

  - The correct way is to add your pluging name on `loadPlugins_list`

The original line should be something like this:
`loadPlugins_list macro,profiles,breakTime,raiseStat,raiseSkill,map,reconnect,eventMacro,item_weight_recorder,xconf`

Adding bus pluging should be something like this:
`loadPlugins_list macro,profiles,breakTime,raiseStat,raiseSkill,map,reconnect,eventMacro,item_weight_recorder,xconf,busCommands.pl`

Deppending on what pluging you want to use, the main plugins are:
  - busCommands
  - busFollow
  - busParty
  
