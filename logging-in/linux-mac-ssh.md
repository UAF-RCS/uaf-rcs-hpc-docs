# Linux / Mac SSH

Linux and Mac users should use the OpenSSH client which is already installed on your computer. Open a terminal session and run the following command to connect to Chinook:

`$ ssh uausername@chinook.alaska.edu`

replacing `uausername` with your UA username \(e.g. jsmith2\).

To enable graphical displays through an X Window, run the following command:

`$ ssh -Y uausername@chinook.alaska.edu`

Unlike Linux, Mac operating systems do not come with an X Window server pre-installed. If you want to display X Windows from Chinook, we recommend installing [XQuartz](https://www.xquartz.org/) on your Mac.

