# TerrariaService
Service script for Terraria dedicated servers on Raspberry Pi OS or other OSes.
This service script lets you start, stop and save the server while running it in the background to avoid using programs like tmux and screen.
Additionally you can use the script to invoke the terraria server commands kick, ban, password, version, time, port, maxplayers, say, motd, dawn, noon, dusk, midnight and settle.

## Setup
Make sure that you have downloaded the dedicated terraria server from [the official Wiki](https://terraria.wiki.gg/wiki/Server#Downloads) and followed the ["How to (RPI / Others OSes)"](https://terraria.wiki.gg/wiki/Server#How_to_(RPI_/_Others_OSes)) there before using the TerrariaService.

### Repository and configuration files
```bash
# Clone the repository to a directory such as /opt/
$ git clone https://github.com/Arceden/TerrariaService
$ cd TerrariaService/
```

```bash
# Copy the example files without the example extension.
$ cp config.cfg.example config.cfg
$ cp terraria.service.example terraria.service
```
You can now edit the files to fit your needs.

### Systemd setup
```bash
# Create symbolic link for systemctl
$ ln -s /opt/TerrariaService/terraria.service /etc/systemd/system/terraria.service
$ systemctl daemon-reload

# Test the service
$ systemctl status terraria
> Active: inactive (dead)

# Enable auto startup (optional)
$ systemctl enable terraria
```

### Local bin
It is recommended to make a symbolic link in the local bin in order to use the terraria service comands.
```bash
# Create symbolic link for the local bin
$ ln -s /opt/TerrariaService/terraria /usr/local/bin/terraria

# Example usage
terraria help
```

### Validate files
Before starting the service, run the following command to avoid problems with missing files or wrong permissions. If it does not work, try fixing it manually with ```chown```.
```bash
# Validate server and service files
$ terraria checkfiles
```

## Usage
Available service commands
Command|Description
-|-
start|Starts the server
stop|Stops the server
checkfiles|Validates the service and server files
state|Displays the server state
kill|Kills the server process
help|Shows the help message

Available server commands
Command|Description
-|-
save|Save the game world
exit|Save the world and stops the server
kick <"player name">|Kicks a player from the server
ban <"player name">|Bans a player from the server
password|Show password
password <"pass">|Change password
version|Print version number
time|Display game time
port|Print the listening port
maxplayers|Print the max number of players
say <"message">|Send a message to all players. They will see the message in yellow prefixed with <server> in the chat
motd|Print MOTD
motd <"message">|Change MOTD
dawn|Change time to dawn (4:30 AM)
noon|Change time to noon (12:00 PM)
dusk|Change time to dusk (7:30 PM)
midnight|Change time to midnight (12:00 AM)
settle|Settle all water
