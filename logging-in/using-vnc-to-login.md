# Using VNC to Login

To run graphical applications on RCS systems remotely, the Virtual Network Computing \(VNC\) application is available and provides some advantages beyond using X Windows over SSH such as a detachable session and better performance over a slow speed connection. Here is basic set up information required for this approach.

\*\*\*Important Note: Please follow all of these steps with each new VNC session.\*\*\*

#### Step 1: Install VNC on your local system <a id="vncstep1"></a>

There are multiple VNC viewer programs available with unique interfaces and features. The application on RCS systems is TigerVNC.

MAC users can use the built in Apple "Screen Sharing" as a VNC client and do not have to install an additional client.

After installing the software, make sure ports 5900 and 5901 are open to allow VNC traffic through your host firewall.

#### Step 2: Setup port forwarding over SSH for the VNC session <a id="vncstep2"></a>

On Linux or MAC systems:

```text
local$ ssh -L 5901:localhost:5901 username@remote.alaska.edu
```

On a Windows system:

Setup a SSH tunnel with PuTTY on Windows.

1. On the left side of the PuTTY dialog box when you open PuTTY, choose Connection-&gt;SSH-&gt;Tunnels
2. in Source Port enter 5901
3. in Destination enter remote.alaska.edu:5901
4. Click Add and you should see the following in the list of forwarded ports:  L5901 remote.alaska.edu:5901

#### Step 3: Connect to the remote system and start the VNC server <a id="vncstep3"></a>

Log onto the remote system over SSH and specify the appropriate ports for VNC client \(your local system\) and server \(remote system\) communication.

Launch a VNC server instance on the remote system. The initial vncserver instance will prompt you for a password to protect your session. Subsequent launches of vncserver will use the same password and you will not be prompted for a password.

```text
remote$ vncserver -localhost

You will require a password to access your desktops.
Password:
Verify:

New 'remote:1 (username)' desktop is remote:1

Creating default startup script /u1/uaf/username/.vnc/xstartup
Starting applications specified in /u1/uaf/username/.vnc/xstartup
Log file is /u1/uaf/username/.vnc/remote:1.log
```

#### Step 4: Open VNC on your local system <a id="vncstep4"></a>

1. Launch Apple "Screen Sharing" on a MAC.

   The Apple "Screen Sharing" connect to server dialog can be accessed with {apple key} K or Finder - Go - Connect to Server. Use "vnc://localhost:5901" as the "Server Address".

2. Launch VNC on Windows from the menu or a launcher icon.

   On Windows, the VNC application should have installed a launcher somewhere in the menus and may have also installed an icon on the desk or start bar depending on options you chose when installing. Use the menu or icon to start VNC.

3. Launch Linux VNC viewer from the command line

   Launch your VNC viewer program and connect to host "localhost" and port 5901. The example below shows how to launch the client using TigerVNC.

   local$ vncviewer localhost:5901

If you are using the TigerVNC GUI, enter "localhost:5901" into the "VNC server:" box then click the "Connect" button. You will then be prompted for the password created in Step 2. If your local VNC client connects successfully, you will then see your desktop on the remote system.

Your circumstances might require the use of different ports due to firewall issues or if you are running more than one VNC server session on the remote system. \(Other people on the system might be running their own sessions as well and occupying the ports.\) If this is the case, you may need to specify port 5902 or 5903 or ... Add 5900 to the display number to determine the correct remote port to use.

To determine whether the VNC viewer has successfully connected, check the log file noted when vncserver was started on the remote system.

After starting the server, the option exists to log out and back in again using different port forwarding parameters.

Note that some VNC viewer programs can automatically set up the SSH port forwarding through a command-line flag such as "-via" or some option in a graphical configuration menu.

#### Step 5: When finished, close the VNC session <a id="vncstep5"></a>

To close your VNC session, view the open sessions on the remote system, then close the appropriate one.

```text
remote$ vncserver -list
TigerVNC server sessions:
X DISPLAY #     PROCESS ID
:1                    252550
remote$ vncserver -kill :1
```

#### Troubleshooting <a id="vnctrouble"></a>

1. Orphaned Session

   If a previous VNC session remains open on the remote system, that old session will need to be closed prior to establishing a new connection using the same port. To identify and kill the old session, first obtain the processID of the "Xnvc" process, then issue the kill command.

   ```text
   remote$ ps -elf | grep username | grep Xvnc
   0 S username    236193      1  0  80   0 - 24842 poll_s Nov09 ?        
         00:00:10 /usr/bin/Xvnc :1 -desktop remote:1 (username) 
         -auth /u1/uaf/username/.Xauthority -geometry 1024x768 
         -rfbwait 30000 -rfbauth /u1/uaf/username/.vnc/passwd 
         -rfbport 5901 -fp catalogue:/etc/X11/fontpath.d -pn -localhost
   remote$ kill 236193
   ```

2. Locked Session

   Depending on your desktop settings on the remote system, the X screensaver may kick in and lock the session after a period of inactivity. If this happens, you'll be prompted for a password that doesn't exist. The xlock process can be killed from the command line. We recommend disabling X locking in the VNC displayed desktop settings to avoid this happening.

3. Reset Server Password

   To change the VNC server password, use the 'vncpasswd' command on the remote system.

4. More Information

   Run 'vncserver --help' and 'man vncserver' for more information on how to use the application.



