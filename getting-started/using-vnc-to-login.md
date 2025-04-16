# Using VNC to Login

To run graphical applications remotely, the Virtual Network Computing (VNC) application is available and provides some advantages beyond using X Windows over SSH such as a detachable session and better performance over a slow speed connection. Here is basic set up information required for this approach.

\*\*\*Important Note: Please follow all of these steps with each new VNC session.\*\*\*

### Install VNC on your local system

There are multiple VNC viewer programs available with unique interfaces and features. The application on RCS hosted systems is TigerVNC ([https://tigervnc.org/](https://tigervnc.org/)). TigerVNC clients are available for Linux and Windows. Mac users can use the built in Apple "Screen Sharing" as a VNC client and do not have to install an additional client.

### A. Launch a VNC Desktop Session

1. Login to a remote system via SSH. The host name is $HOST in the steps below.
2. Set a VNC password (six to eight characters):\
   `$ vncpasswd`
3. Launch the session:\
   `$ vncserver -xstartup /usr/bin/startxfce4 -SecurityTypes VncAuth,TLSVnc -geometry 1600x1280 -localhost yes`
4. Note the X display number for your session:\
   `$ vncserver -list`
5. Log off:\
   `$ exit`

If Gnome is the preferred desktop, use /usr/bin/gnome-session instead of /usr/bin/startxfce4 in step A.3.

### B. Connect VNC Client from macOS Using an SSH Tunnel

1. The remote port to connect to is the "RFB Port #" in the output from step A.4 above. This value is $RPORT in the next step. If "RFB Port #" is not in the output, take the "X Display #" and add 5900 to it.
2. In a Terminal window, establish an SSH tunnel:\
   `$ ssh -L 59000:localhost:$RPORT -C $HOST`
3. In Finder, launch the remote desktop client by choosing Go->Connect to Server from the menu or press Cmd-K.
4. Enter vnc://localhost:59000 for the server and click Connect.
5. Enter the VNC password set in step A.2 above and click Sign In. A window with your personal desktop on the remote host should open.

### C. Connect VNC Client from Linux Using an SSH Tunnel

1. If needed, install a VNC viewer on your Linux system. A commonly available one is TigerVNC.
2. The remote port to connect to is the "RFB Port #" in the output from step A.4 above. This value is $RPORT in the next step. If "RFB Port #" is not in the output, take the "X Display #" and add 5900 to it.
3. In an Xterm window, establish an SSH tunnel:\
   `$ ssh -L 59000:localhost:$RPORT -C $HOST`
4. In a second Xterm window, launch the VNC viewer:\
   `$ vncviewer localhost::59000`
5. Enter the VNC password set in step A.2 above and click Sign In. A window with your personal desktop on the remote host should open.

### D. Connect VNC Client from Windows Using an SSH Tunnel

1. If needed, download & install a VNC viewer on your Windows system from https://tightvnc.com/download.php.
2. The remote port to connect to is the "RFB Port #" in the output from step A.4 above. This value is $RPORT in the next step. If "RFB Port #" is not in the output, take the "X Display #" and add 5900 to it.
3. In a command prompt window, establish an SSH tunnel:\
   `$ ssh -L 59000:localhost:$RPORT -C $HOST`
4. Launch TightVNC Viewer.
5. Enter localhost::59000 for the remote host and click Connect.
6. Enter the VNC password set in step A.2 above and click OK. A window with your personal desktop on the remote host should open.

### When Finished, Close the VNC Desktop Session <a href="#vncstep5" id="vncstep5"></a>

The remote desktop window can be closed at any time. Exit the SSH tunnel session then close the remote desktop window. This does not interrupt the remote desktop session. It will remain until you log out from it or the workstation is rebooted. To reconnect to the remote desktop session, repeat the steps in section B, C, or D. A screen lock may be enabled when you reconnect. Enter your UA password to unlock. To close your VNC session, view the open sessions on the remote system, then close the appropriate one.

```
host$ vncserver -list
TigerVNC server sessions:
X DISPLAY #     PROCESS ID
:1                    252550
remote$ vncserver -kill :1
```

### Troubleshooting <a href="#vnctrouble" id="vnctrouble"></a>

Your circumstances might require the use of different ports due to firewall issues or if you are running more than one VNC server session on the remote system. (Other people on the system might be running their own sessions as well and occupying the ports.) If this is the case, you may need to specify port 5902 or 5903 or ... Add 5900 to the display number to determine the correct remote port to use.

To determine whether the VNC viewer has successfully connected, check the log file noted when vncserver was started on the remote system.

After starting the server, the option exists to log out and back in again using different port forwarding parameters.

Note that some VNC viewer programs can automatically set up the SSH port forwarding through a command-line flag such as "-via" or some option in a graphical configuration menu.

1.  Orphaned Session

    If a previous VNC session remains open on the remote system, that old session will need to be closed prior to establishing a new connection using the same port. To identify and kill the old session, first obtain the processID of the "Xnvc" process, then issue the kill command.

    ```
    host$ ps -elf | grep username | grep Xvnc
    0 S username    236193      1  0  80   0 - 24842 poll_s Nov09 ?        
          00:00:10 /usr/bin/Xvnc :1 -desktop remote:1 (username) 
          -auth /u1/uaf/username/.Xauthority -geometry 1024x768 
          -rfbwait 30000 -rfbauth /u1/uaf/username/.vnc/passwd 
          -rfbport 5901 -fp catalogue:/etc/X11/fontpath.d -pn -localhost
    host$ kill 236193
    ```
2.  Locked Session

    Depending on your desktop settings on the remote system, the X screensaver may kick in and lock the session after a period of inactivity. If this happens, you'll be prompted for a password that doesn't exist. The xlock process can be killed from the command line. We recommend disabling X locking in the VNC displayed desktop settings to avoid this happening.
3.  Banish Authentication Popup

    If you get a "Authentication is required to set the network proxy used for downloading packages" dialog box constantly opening, launch a Terminal Console and type gnome-session-properties and then uncheck the PackageKit Update Applet. You may need to restart your VNC session for this to take effect.
4.  Reset Server Password

    To change the VNC server password, use the 'vncpasswd' command on the remote system.
5.  More Information

    Run 'vncserver --help' and 'man vncserver' for more information on how to use the application.
