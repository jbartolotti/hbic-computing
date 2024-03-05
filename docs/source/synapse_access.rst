Synapse Server Access
======================

.. _synapse_request_access:

Requesting Access
-----------------------

Submit an `access request <https://redcap.kumc.edu/surveys/?s=R7PCHA3PNL>`_ for yourself or others for Synapse, the VPN (required for Non-KUMC/KU-L users or KUMC students), or R/P Network drives.

.. _synapse_access:

Accessing Synapse
------------------------

Windows
----------------------

#. Install `MobaXterm <https://mobaxterm.mobatek.net/download-home-edition.html>`_ or your preferred SSH client. If you do not have software installation rights on your PC, you may use the Portable edition which contains a stand-alone .exe file that does not need to be installed. Otherwise, select the Installer edition.
#. Open MobaXterm and configure a new session. Select SSH, ensure X11-Forwarding is checked, and enter the following information:
   
   * Remote Host: hbic-synapse2.kumc.edu
   
   * Username: <your KUMC username> *Note: admins need to login with their sa-USERNAME account*

   .. image:: media/mobaxterm_1.png
     :width: 800
     :alt: A screenshot of MobaXterm. A red circle is drawn around the "Session" button on the top row of the application. A pop-up window titled "Session settings" is opened, and there is a red circle drawn around the "SSH" tab. In the section Basic SSH settings, the field Remote host is circled and contains the text "hbic-synapse2.kumc.edu". A red circle is drawn around the specify username field. The filed is checked and contains an example username, a123b456. In the panel below, the "Advanced SSH settings" tab is selected. A red circle is drawn around the option X-11 forwarding, and this option is checked.

#. Connect to Synapse by clicking the Sessions tab on the Left, and then selecting the hbic-synapse2.kumc.edu session that you just configured. Enter your KUMC credentials when prompted.

Mac OS
-------------------------

#. Install XQuartz. For Macs with an M1 CPU, XQuartz displays have a `common issue <https://github.com/XQuartz/XQuartz/issues/31>`_ where a black screen or no screen is displayed. To address this issue, use one of the following workarounds:

   * Use X2Go to access Synapse (see section further below on this page)
   
   * Apply the supported fix from IT (Shijil Raveendran sraveendran at kumc dot edu). First, install XQuartz 2.8.5 and modify the following two settings in the Xquartz preference file org.xquartz.X11: 1) Set the enable_igx property to 1 with the command “defaults write org.xquartz.X11 enable_iglx -bool true”. 2) Set the enable_render_extension property to 0 with the command “defaults write org.xquartz.X11 enable_render_extension 0”.
   
   * The above fix has been implemented in an XQuartz installer available in the KUMC Self Service application installer. Open the Self Service app in your Applications folder and login. Under the productivity category you should see the XQuartz application available to install. Installing it will remove any existing XQuartz application, install the latest version i.e. 2.8.5, and then add the two settings that fixed the issue.

   .. image:: media/xquartz.png
     :width: 800
     :alt: A screenshot of the KUMC Self Service application installer. A red box is drawn around the "Productivity" item in the category list on the left hand pane. In the productivity category, a red box is drawn around the entry for XQuartz, which includes the button Reinstall.

#. Open the Terminal application, and at the command prompt, enter the following command and press return. Enter your password when prompted. The ssh command with the -Y option specified will allow X-Windows forwarding during your SSH session.

   .. code_block:: console
     ssh -Y <username>@hbic-synapse2.kumc.edu

   .. image:: media/macos_2.jpg
     :width: 800
     :alt: A screenshot of the Terminal application on Mac that successfully connected to Synapse using the command, ssh -X username@hbic-synapse2.kumc.edu

#. The first time that you login to synapse, confirm that X-Windows forwarding is working. Enter xeyes on the terminal and press return. You should get a window with a pair of eyes open on your screen.

   .. image:: media/xeyes.jpg
     :width: 200
     :alt: The xeyes window, showing eyes that follow the user's cursor around the screen.
