# Remote Desktop Connection Manager v3.12
# https://learn.microsoft.com/en-us/sysinternals/downloads/rdcman

Summarize this article for me
By Julio Rosales 

Published: July 14, 2026

Download Download Remote Desktop Connection Manager (116.1 MB)
Run now from Sysinternals Live.

Introduction
RDCMan manages multiple remote desktop connections. It is useful for managing server labs where you need regular access to each machine such as automated checkin systems and data centers.

Servers are organized into named groups. You can connect or disconnect to all servers in a group with a single command. You can view all the servers in a group as a set of thumbnails, showing live action in each session. Servers can inherit their logon settings from a parent group or a credential store. Thus when you change your lab account password, you only need to change the password stored by RDCMan in one place. Passwords are stored securely by encrypting with either CryptProtectData using the (locally) logged on user's authority or an X509 certificate.

User with OS versions prior to Win7/Vista will need to get version 6 of the Terminal Services Client. You can obtain this from the Microsoft Download Center: XP; Win2003

Upgrade note: RDG files with this version of RDCMan are not compatible with older program versions. Any legacy RDG file opened and saved with this version will be backed up as filename.old

The Display
The Remote Desktop Connection Manager display consists of the menu, a tree with groups of servers, a splitter bar, and a client area.

The Menu
There are several top-level menus in RDCMan:

File - load, save, and close RDCMan file groups
Edit - add, remove, and edit the properties of servers and groups.
Session - connect, disconnect and log off sessions
View - options to control the visibility of the server tree, virtual groups and size of the client area
Remote Desktops - allows access to the groups and servers in a hierarchical fashion, similar to the server tree; primarily useful when the Server Tree is hidden
Tools - change application properties
Help - learn about RDCMan (you probably already found this)
The Tree
Most work, such as adding, removing, and editing servers and groups, can be accomplished via right-clicking on a tree node. Servers and groups can be moved using drag-and-drop.

Keyboard shortcuts:

Enter: Connect to selected server.
Shift+Enter: Connect to the selected server using the Connect As feature.
Delete: Remove selected server or group.
Shift+Delete: Remove selected server or group without question.
Alt+Enter: Open properties dialog for selected server or group.
Tab: If a connected server is selected, give it focus.
Use the [View.Server tree location] menu option to locate the tree at the left or right edge of the window.

The server tree can be docked, auto-hidden, or always hidden via the [View.Server tree visibility] menu option. When the server tree is not displayed, servers can still be accessed through the Remote Desktops menu. When the tree is auto-hidden, the splitter bar remains visible at the left side of the window. Hovering over it will bring the server tree back into view.

The Client Area
The client area display depends on the node selected in the tree. If a server is selected, the client area shows the remote desktop client for that server. If a group is selected, the client area shows a thumbnail of the servers within that group. The size of the client area can be specified via the View menu, as well as resizing the RDCMan window. Use [View.Lock window size] to prevent the window from being resized by dragging the frame.

Caution: Connected servers can receive focus from keyboard navigation of the thumbnail view. It is not always obvious which server has focus, so be careful. There is a setting to control this: [Display Settings.Allow thumbnail session interaction].

Full Screen Mode
To work with a server in full screen mode, select the server to give it focus and press Ctrl+Alt+Break (this key is configurable, see Shortcut Keys.) To leave full screen mode, press Ctrl+Alt+Break again or use the minimize/restore buttons in the connection title bar. Multiple monitors can be spanned if enabled by the monitor spanning option.

Shortcut Keys
You can find the full list of Terminal Services shortcut keys here. Some of these can be configured from the Hot Keys tab.

Files
The top-level unit of organization in RDCMan is a remote desktop file group. File groups are collections of groups and/or servers that are stored in a single physical file. Servers can't live outside of a group and groups can't live outside of a file.

A file has all the characteristics of a server group other than being able to change its parent.

Groups
A group contains a list of servers and configuration information such as logon credentials. Configuration settings can be inherited from another group or the application defaults. Groups can be nested but are homogeneous: a group may either contain groups or servers, but not both. All the servers in a group can be connected or disconnected at once.

When a group is selected in the tree view, the servers underneath it are displayed in a thumbnail view. The thumbnails can show the actual server windows or simply the connection status. Global thumbnail view properties can be adjusted via the [Tools.Options.Client Area] tab while group/server-specific settings are in Display Settings.

Smart Groups
Smart groups are populated dynamically based on a set of rules. All ancestors of sibling groups of the smart group are eligible for inclusion.

The Connected Virtual Group
When a server is in the connected state, it is automatically added the to Connected virtual group. Servers cannot be explicitly added or removed from the Connected group.

The Connected group can be toggled on/off via the View menu.

The Reconnect Virtual Group
There are sometimes situations where a server disconnects and will be intentionally offline for an unspecified length of time, e.g. when rebooting after an OS update. When this is the case, drag the server in question to the Reconnect group. RDCMan will continually attempt to connect to the server until it is successful.

The Reconnect group can be toggled on/off via the View menu.

The Favorites Virtual Group
The Favorites virtual group is a flat file of your favorite servers. You can add any server from the server tree. This is helpful when you have many servers in the tree and often work with a handful of servers from different groups.

The Favorites group can be toggled on/off via the View menu.

The Connect To Virtual Group
The Connect To Virtual Group contains the servers that are not members of user-created groups. See Ad Hoc Connections for details.

The Connect To group is visible while ad hoc connections exist and disappears when there are none.

The Recent Virtual Group
The Recent Virtual Group contains the servers that have been recently accessed.

The Recent group can be toggled on/off via the View menu.

Servers
A server has a server name (the computer's network name or IP address), an optional display name, and logon information. The logon information may be inherited from another group.

Adding Servers Manually
Servers names following a pattern can be bulk added to a group. There are two pattern classes:

Iteration - {a,b,c} iterates over the comma-delimited contents.
Range - [1-5] iterates the numerical range. Prefix the lower bound with 0's to specify the minimum width.
Examples:

server1{a,b,c}: Adds server1a, server1b, server1c
server[001-15]: Adds server001, server002, ..., server015
{dca,dcb}rack[1-5]sql[1-2]: Adds dcarack1sql1, dcarack1sql2, dcarack2sql1, ..., dcarack5sql2, dcbrack1sql1, ... dcbrack5sql2
