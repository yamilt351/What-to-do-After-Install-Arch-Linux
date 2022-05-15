                      #ARCH LINUX 

##inslling gnome extra themes
*sudo pacman -S gnome  gnome-extra-themes flatpak* // restart

                #video hardware aceleration

*sudo pacman -S libva-intel-driver intel-gpu-tools libva-utils*

##Firefox configuration:
<dl>
<dt>gfx.webrender.all           --) true</dt>  
<dt>media.ffmpeg.vaapi.enabled  --) true</dt>
<dt>media.ffvpx.enabled         --) false</dt>
<dt>media.rdd-vpx.enabled       --) false</dt>
<dt>media.av1.enabled           --) false</dt>
</dl>

    ##X11:

*export MOZ_X11_EGL=1 && export MOZ_DISABLE_RDD_SANDBOX=1 && export MOZ_LOG="PlatformDecoderModule:5" && firefox*

    ##WAYLAND:
    
*export MOZ_ENABLE_WAYLAND=1 && export MOZ_DISABLE_RDD_SANDBOX=1 && export MOZ_LOG="PlatformDecoderModule:5" && firefox*



          #Adding envirnment variables system wide (Then restart)

*sudo nano /etc/environment*

*Add the following line to /etc/environment*
                     ##For X11:
*export MOZ_X11_EGL=1* 
*export MOZ_DISABLE_RDD_SANDBOX=1*


                    ##For WAYLAND:

*export MOZ_ENABLE_WAYLAND=1*
*export MOZ_DISABLE_RDD_SANDBOX=1*
_____________________________________________________________
                    #INTEL DRIVERS
<dl>                   
<dt>sudo pacman -S intel-ucode</dt>
<dt>sudo grub-mkconfig -o /boot/grub/grub.cfg</dt>
</dl>

#Set up firewall
<dl>
<dt>Install ufw:</dt>
<dt>sudo pacman -S ufw</dt>

<dt>Enable it.</dt>
<dt>sudo ufw enable </dt>

<dt>Check its status:</dt>
<dt>sudo ufw status verbose</dt>

<dt>Enable the start-up with the system:</dt>
<dt>sudo systemctl enable ufw.service</dt>
<dt> restart</dt>
</dl>

#multilib enabling

-   sudo nano /etc/pacman.conf 

#discoment multilib

- sudo pacman -Syyuu


#nvidia setting and gaming

*sudo pacman -Syu nvidia nvidia-utils lib32-nvidia-utils lib32-opencl-nvidia opencl-nvidia libvdpau libxnvctrl vulkan-icd-loader lib32-vulkan-icd-loader mesa lib32-mesa
libva-mesa-driver mesa-vdpau opencl-mesa vulkan-mesa-layers mesa-demos
vulkan-tools lib32-libva-mesa-driver lib32-mesa-vdpau lib32-opencl-mesa
lib32-vulkan-mesa-layers lib32-mesa-demos wine-gecko wine-mono winetricks vulkan opengl lib32-gst-plugins-base lib32-gst-plugins-good meson systemd git dbus libinih
lib32-gamemode gamemode llib32-systemd   nvidia-settings opencl-headers*

*sudo pacman -Syu wine-staging giflib lib32-giflib libpng lib32-libpng libldap
lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils
lib32-v4l-utils libpulse lib32-libpulse libgpg-error lib32-libgpg-error alsa-plugins
lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo
sqlite lib32-sqlite libxcomposite lib32-libxcomposite libxinerama lib32-libgcrypt
libgcrypt lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader
lib32-opencl-icd-loader libxslt lib32-libxslt libva  gtk3 lib32-gtk3
gst-plugins-base-libs lib32-gst-plugins-base-libs*

#game mode
-	git clone https://github.com/FeralInteractive/gamemode.git
-	cd gamemode*
-	git checkout 1.6.1* check the version before
-	./bootstrap.sh*


#xorg-drivers
*sudo pacman -S xorg-drivers*

#Lutris
* enviroment variables:
Key:
__GL_SHADER_DISK_CACHE_SKIP_CLEANUP
Value
1
 command prefix :
gamemoderun DXVK_HUD=60*
