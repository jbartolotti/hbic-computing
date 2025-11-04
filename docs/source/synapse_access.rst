Synapse Server Access
======================

.. _synapse_request_access:

Requesting Access
-----------------------

Submit an `access request <https://redcap.kumc.edu/surveys/?s=R7PCHA3PNL>`_ for yourself or others for Synapse, the VPN (required for Non-KUMC/KU-L users or KUMC students), or R/P Network drives.

.. _synapse_access:

Accessing Synapse
------------------------

**ATTENTION:** hbic-synapse**2** has been deprecated. Please direct your connections to **hbic-synapse.kumc.edu** (no number). Direct questions to jbartolotti2 at kumc dot edu.

Windows
----------------------

#. Install `MobaXterm <https://mobaxterm.mobatek.net/download-home-edition.html>`_ or your preferred SSH client. If you do not have software installation rights on your PC, you may use the Portable edition which contains a stand-alone .exe file that does not need to be installed. Otherwise, select the Installer edition.
#. Open MobaXterm and configure a new session. Select SSH, ensure X11-Forwarding is checked, and enter the following information:
   
   * Remote Host: hbic-synapse.kumc.edu
   
   * Username: <your KUMC username> *Note: admins can login with their USERNAME or sa-USERNAME account*

   .. image:: media/mobaxterm_1.png
     :width: 800
     :alt: A screenshot of MobaXterm. A red circle is drawn around the "Session" button on the top row of the application. A pop-up window titled "Session settings" is opened, and there is a red circle drawn around the "SSH" tab. In the section Basic SSH settings, the field Remote host is circled and contains the text "hbic-synapse.kumc.edu". A red circle is drawn around the specify username field. The filed is checked and contains an example username, a123b456. In the panel below, the "Advanced SSH settings" tab is selected. A red circle is drawn around the option X-11 forwarding, and this option is checked.

#. Connect to Synapse by clicking the Sessions tab on the Left, and then selecting the hbic-synapse.kumc.edu session that you just configured. Enter your KUMC credentials when prompted.

Mac OS
-------------------------

#. Install XQuartz. For Macs with an M1 CPU, XQuartz displays have a `common issue <https://github.com/XQuartz/XQuartz/issues/31>`_ where a black screen or no screen is displayed. To address this issue, use one of the following workarounds:

   * Use X2Go to access Synapse (see section further below on this page)
   
   * Apply the supported fix from IT (Shijil Raveendran sraveendran at kumc dot edu). First, install XQuartz 2.8.5 and modify the following two settings in the Xquartz preference file org.xquartz.X11: 1) Set the enable_igx property to 1 with the command “defaults write org.xquartz.X11 enable_iglx -bool true”. 2) Set the enable_render_extension property to 0 with the command “defaults write org.xquartz.X11 enable_render_extension 0”.
   
   * The above fix has been implemented in an XQuartz installer available in the KUMC Self Service application installer. Open the Self Service app in your Applications folder and login. Under the productivity category you should see the XQuartz application available to install. Installing it will remove any existing XQuartz application, install the latest version i.e. 2.8.5, and then add the two settings that fixed the issue.

   .. image:: media/xquartz2.png
     :width: 800
     :alt: A screenshot of the KUMC Self Service application installer. A red box is drawn around the "Productivity" item in the category list on the left hand pane. In the productivity category, a red box is drawn around the entry for XQuartz, which includes the button Reinstall.

#. Open the Terminal application, and at the command prompt, enter the following command and press return. Enter your password when prompted. The ssh command with the -Y option specified will allow X-Windows forwarding during your SSH session.

   .. code-block:: console

     ssh -Y <username>@hbic-synapse.kumc.edu



#. The first time that you login to synapse, confirm that X-Windows forwarding is working. Enter xeyes on the terminal and press return. You should get a window with a pair of eyes open on your screen.

   .. image:: media/xeyes.jpg
     :width: 200
     :alt: The xeyes window, showing eyes that follow the user's cursor around the screen.


Azure Virtual Desktop
-----------------------------

#. Some graphical software on Synapse may fail to load on certain MacOS configurations. Instead, you can use Azure Virtual Desktop to access a virtual Windows environment to connect to Synapse, as well as the R- and P- Drives and certain pre-installed University software.
#. `Request access <https://redcap.kumc.edu/surveys/?s=R7PCHA3PNL>`_ to the R-Drive "Resources" folder (R:\Hoglund\Resources) 
#. Connect to the Azure Virtual Desktop.
#. Open a File Explorer window and navigate to R:\Hoglund\Resources\Applications\MobaXterm_Portable_v25.3 and open MobaXterm_Personal_25.3.exe. If you receive a security warning, first verify that the indicated R-Drive path in the pop-up is correct, then Run the software. 
#. In MobaXterm, configure a new session. Select SSH, ensure X11-Forwarding is checked, and enter the following information:
   
   * Remote Host: hbic-synapse.kumc.edu
   
   * Username: <your KUMC username> *Note: admins can login with their USERNAME or sa-USERNAME account*

   .. image:: media/mobaxterm_1.png
     :width: 800
     :alt: A screenshot of MobaXterm. A red circle is drawn around the "Session" button on the top row of the application. A pop-up window titled "Session settings" is opened, and there is a red circle drawn around the "SSH" tab. In the section Basic SSH settings, the field Remote host is circled and contains the text "hbic-synapse.kumc.edu". A red circle is drawn around the specify username field. The filed is checked and contains an example username, a123b456. In the panel below, the "Advanced SSH settings" tab is selected. A red circle is drawn around the option X-11 forwarding, and this option is checked.

#. Connect to Synapse by clicking the Sessions tab on the Left, and then selecting the hbic-synapse.kumc.edu session that you just configured. Enter your KUMC credentials when prompted.


X2Go
------------------------------

`X2Go <https://wiki.x2go.org/doku.php/doc:newtox2go>`_ is Remote Desktop software that connects to the Synapse server with a graphical interface suitable for low-bandwidth connections or over a VPN. **If application windows on Synapse are slow or unresponsive, use X2Go to connect**

#. Install X2Go by obtaining the `X2GoClient application <https://wiki.x2go.org/doku.php/doc:installation:x2goclient>`_ for Windows or Mac. 

   **IMPORTANT:** The Windows X2Go Client requires administrator rights to install. If you do not have admin rights, you can obtain a portable version (non-installing .exe) from the R-Drive Resources folder, R:/Resources/HBIC-Computing/X2Go/X2GoClient.zip. Copy and unzip the file to your computer and run the x2goclient.exe file.

#. Open X2Go and under the Session tab, click New Session (Ctrl-N) and configure as follows: 

   **Session tab**

   * Host: hbic-synapse.kumc.edu

   * Login: <your KUMC username, e.g. j186b025>

   * SSH port: 22

   * Session Type: Custom desktop

   * Command: startxfce4

   **Connection tab**

   * Connection speed: LAN

   **Input/Output tab**

   * Display: Select Fullscreen or define a Custom window size that is smaller than your current display.

   *Note: To open a terminal instead of a graphical desktop, change Session Type to Single application, Terminal*

#. After creating the session, select it from the dock on the right and login with your KUMC username and password. This will open a desktop with a menu bar at the bottom. Click the Red Hat icon and select from the available applications. 
   * Applications: Select from Science, Education, or Other. If the application you need is not present, start it from the Terminal application directly.
   
   * Terminal: Under System Tools, select Xfce Terminal, XTerm, or QTerminal. You can use these terminals the same as you would connecting to Synapse directly using MobaXTerm or Terminal, but graphical applications will be faster and more responsive.

   * File Browser: Open your home folder (your username) from the desktop. If it is not present, right-click the desktop, select Desktop Preferences, and under the Advanced tab, click the checkbox next to Home and press OK. If the R or P drives are not visible, first mount them using the terminal. Click the Red Hat icon on the bottom menu, and select Xfce Terminal under System Tools. Run the command *sudo KUMC-Map R* (or P, or KUL, etc.).

   * XNAT: Select Firefox from Internet, and navigate to https://xnat.kumc.edu
