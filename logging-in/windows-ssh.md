# Windows SSH

Windows users will need to download and install a third-party SSH client in order to log into Chinook. Here are a few available options:

* [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/) \(open source, MIT license\)
* [Secure Shell](https://alaska.edu/oit/software/authenticate/files/windows-applications/secure-shell/) \(proprietary, UA credentials required for download\)

#### Installing PuTTY <a id="installing-putty"></a>

RCS recommends that Windows users download and install PuTTY, a free-and-open-source ssh/rsh/telnet client.

1. Download PuTTY from [the official site](http://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
2. Run the PuTTY installer, and select "Next".
3. By default, the installer will install in `C:\Program Files (x86)\PuTTY` under 64-bit Windows, and `C:\Program Files\PuTTY` under 32-bit Windows. Select "Next".
4. The installer will prompt you for a Start Menu folder in which to create shortcuts. Select "Next".
5. Select "Create a desktop icon for PuTTY", and select "Next".
6. The installer will allow you to review your choices. Select "Install" after you have done so.
7. The installer will require only a few seconds to install PuTTY on your computer. Select "Finish". As it closes, the installer will by default open PuTTY's readme file, which contains additional information on using the additional tools included with PuTTY.

#### Using PuTTY <a id="using-putty"></a>

Establishing a remote login session over SSH using PuTTY is reasonably straightforward. The following steps describe how to do this, turn on X11 forwarding, and save connection settings.

#### Remote Login via SSH <a id="remote-login-via-ssh"></a>

1. Open PuTTY using the icon placed on your desktop by the PuTTY installer.
2. For "Host Name", enter `chinook.alaska.edu`.
3. Select "Open" to initiate an SSH connection request.
4. You may receive a security alert warning you that your client cannot establish authenticity of the host you are connecting to. This warning is always displayed the first time your SSH client connects to any computer it has never connected before. If you have never connected to Chinook using this PuTTY installation, select "Yes".
5. A terminal window should open. You will be prompted for a username. Enter your UA username. If you want to avoid entering your UA username every time you log in, you can prefix the hostname you entered earlier with your UA username followed by`@`. As an example, a user named jsmith2 could enter`jsmith2@chinook.alaska.edu`. This is the same`user@host`syntax expected by OpenSSH.
6. You will be prompted for a password. Enter your UA password and continue. Public key authentication is supported by PuTTY via the Pageant tool. If you wish to set up this authentication scheme, please see Chapter 8 of the [PuTTY documentation](https://the.earth.li/~sgtatham/putty/latest/htmldoc/).
7. On successful authentication, a command prompt will appear and allow you to execute commands on Chinook.

#### Enabling Graphics <a id="enabling-graphics"></a>

Some applications on Chinook, especially visualization applications, require a graphical display. It is possible to tunnel graphics over an SSH connection using X11 graphics forwarding, which is supported by PuTTY.

1. Install a local X Window server. We recommend installing the last free version of [XMing](https://sourceforge.net/projects/xming/files/Xming/6.9.0.31/), which became proprietary software in May 2007.
2. In PuTTY, define a connection to `chinook.alaska.edu` and navigate to "Connection-SSH-X11". Check the box labeled "Enable X11 forwarding".
3. Initiate an SSH connection request and log in as outlined in the last section.
4. Ensure that your local X server is running. Without this, any graphical application will fail to run properly.
5. Run `xlogo`, a simple graphical application. If you see a window containing a black X on a white background, you have successfully enabled X11 forwarding.

#### Saving Connection Settings <a id="saving-connection-settings"></a>

1. Configure your connection settings as desired
2. Navigate to "Category-Session"
3. Enter a name for your session in the "Saved Sessions" input box, and select "Save". Your session should now appear as a new line in the text box to the left of "Save".
4. To load saved settings, select the session you want to load and then select "Load".

Optionally, PuTTY's command-line flags allow you to create shortcuts that load a particular connection.

1. Copy your PuTTY shortcut icon
2. Right click on the copy, and select "Properties"
3. In the "Target" field, append `-load` followed by the connection name in quotation marks
4. Select "Apply", and close the window
5. Rename the modified shortcut appropriately

#### Troubleshooting <a id="putty-troubleshooting"></a>

**When I try to connect, PuTTY opens an alert box that says "Disconnected: No supported authentication methods available".**

This message means that authentication by username failed. This is most likely caused by an incorrect username, or because you do not have access to Chinook. Please ensure that you received an email from RCS User Support \([uaf-rcs@alaska.edu](mailto:uaf-rcs@alaska.edu)\) notifying you of your Chinook account creation, and use the username provided in that email.

**My application returns the error "X connection to localhost:10.0 broken \(explicit kill or server shutdown\)" \(or similar\).**

This is an indication that your local X server is not running. Check the icons on the right-hand side of your task bar for the X server icon. If it is not present, ensure that you have installed an X server locally and that it is running. Once the icon is present, try opening your program again.

**I received the "Unknown Host Key" popup alert, followed by another popup stating: "Server unexpectedly closed network connection".**

This indicates that the server's SSH timeout was triggered. SSH servers are often configured to kill incoming connections that do not send data for a while. While you were responding to the "Unknown Host Key" popup, the remote host's connection timeout expired and it disconnected you. You should be able to reconnect without problem.  
  


