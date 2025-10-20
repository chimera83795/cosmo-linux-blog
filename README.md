# cosmo-linux-blog
Experiences with running linux on planet's cosmo communicator. Error Fixes and usable software.
Any additional information and questions are welcome!

## Installation
The linux version I tested include Ubuntu-Touch and Gemian.
The general installation guides can be found here:
1. https://support.planetcom.co.uk/index.php/Linux_for_Cosmo
2. https://github.com/gemian

1. https://devices.ubuntu-touch.io/device/cosmo-communicator/release/xenial/
2. https://github.com/gemian/gemian/wiki/UBPorts

Just to make this clear, at the time of writing this, I used the latest v.4 gemian.
In my case, the gemian installation medium wasn't detected and I had to install a newer android version first.
It also may be important to format the installation drive as NTFS.

After installation login as cosmo/cosmo. When you might need to adjust the keyboard layout.
It might also be a good idea to set the system-locale language to your prefered language using the settings manager.
Without a system-language set, your gemian might change language depending on for example keyboard layout on next boot.
I encountered this problem with the jp-layout. The login-screen still remained in japanese after reloading
and the keyboard layout too, so you might need to press both SHIFT-Keys at the same time to change english characters.

Now when it comes to updating and upgrading, make sure to change the s */etc/apt/sources.list*
from *deb.debian* to *archive.debian* and also modify the */etc/apt/sources.list.d/gemian*.
In my case I commented out the gemian-buster line.
The most important thing to know is that upgrading will break your linux installation,
resulting to it being stuck ad *gemian booting* screen after rebooting.
A solution to this might be to *apt-mark hold* kernel/image packages.
Also *initramfs* should be set to hold. The main issue now is that certain software won't run due to it not meeting dependencies.

To install UBTouch, you also need to install gemian before.
To find the UBTouch installation files may feel a bit unguided and difficult.
https://gitlab.com/ubports/porting/community-ports/android9/planet-cosmocom/planet-cosmocom/-/jobs?kind=BUILD




#### Chromium too small
Locate the UserDependencies flags file and add *--force-device-scale-factor* to your prefered factor and adjust it to the other flags found in the file.
In my case the file was located at */etc/chromium.d/default-flags* and i added:
> export CHROMIUM_FLAGS="$CHROMIUM_FLAGS --force-device-scale-factor=1.8"

Sadly chromium seems to be the best working browser.So I changed the default search-engine to duckduckgo :/ , so
just click on settings -> search engine -> manage -> add -> duckduckgo | duckduckgo.com | https://duckduckgo.com/q=%s
if you want to change the search engine to something a bit more private.

### tor
To access the onion-routing network (tor), installing the service and proxychains default configuration should work fine,
but you should clear the cookies cause unfortunately the only working browser i know of is chromium.

### openssl and libcrypto
If you want to use libcrypto (3) or upgrade your openssl, you might encounter some issues while using apt,
i guess that is since the official gemian repo isnt updated anymore.
Download the desired version from: https://www.openssl-library.org/source/ .
> cd <FILE-LOCATION>

> #extract the archive with tar or whatever compression type you chose.

> cd <EXTRACTED-FOLDER>

> ./config #add desired options

> make

> sudo make install

When link the /usr/local location to /usr/lib/<architecture>.

> sudo ln -s /usr/local/lib/libcrypto.so.3 /usr/lib/<architecture>/libcrypto.so.3

> sudo ln -s /usr/local/lib/libssl.so.3 /usr/lib/<architecture>/libssl.so.3


### other application
deb-packages often have been compiled for a different architecture.
A solution might be to recompile from source, but the way to install depend on the exact package. 














