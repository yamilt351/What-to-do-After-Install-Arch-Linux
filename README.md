# What-to-do-After-Install-Arch-Linux 

*** inslling gnome extra themes
sudo pacman -S gnome-extra-themes

*** delete orphans pakages 
sudo pacman -Rs $(pacman -Qtdq)
pacman -Rsdn $(pacman -Qqdt)

***video hardware aceleration

sudo pacman -S libva-intel-driver intel-gpu-tools libva-utils

Firefox configuration:
1. gfx.webrender.all           --) true
2. media.ffmpeg.vaapi.enabled  --) true
3. media.ffvpx.enabled         --) false
4. media.rdd-vpx.enabled       --) false
5. media.av1.enabled           --) false


 X11:

export MOZ_X11_EGL=1 && export MOZ_DISABLE_RDD_SANDBOX=1 && export MOZ_LOG="PlatformDecoderModule:5" && firefox

    WAYLAND:
    
export MOZ_ENABLE_WAYLAND=1 && export MOZ_DISABLE_RDD_SANDBOX=1 && export MOZ_LOG="PlatformDecoderModule:5" && firefox



Adding envirnment variables system wide:

sudo nano /etc/environment

    Add the following line to /etc/environment
    For X11:
export MOZ_X11_EGL=1 
export MOZ_DISABLE_RDD_SANDBOX=1


 For WAYLAND:

export MOZ_ENABLE_WAYLAND=1
export MOZ_DISABLE_RDD_SANDBOX=1

sudo pacman -S intel-ucode
sudo grub-mkconfig -o /boot/grub/grub.cfg

*****. Disable GRUB delay

Add the following to /etc/default/grub:
**** achieve the fastest possible boot:
GRUB_FORCE_HIDDEN_MENU="true"

Then put file 31_hold_shift to /etc/grub.d/.
Download 31_hold_shift https://goo.gl/nac6Kp

Make it executable, and regenerate the grub configuration:
sudo chmod a+x /etc/grub.d/31_hold_shift
sudo grub-mkconfig -o /boot/grub/grub.cfg

*** Set up firewall

Install ufw:
sudo pacman -S ufw

Enable it.
sudo ufw enable 

Check its status:
sudo ufw status verbose

Enable the start-up with the system:
sudo systemctl enable ufw.service

**** optimize pacman
sudo pacman-optimize

**** multilib enabling

sudo nano /etc/pacman.conf 

discoment multilib

sudo pacman -Syyuu


***nvidia setting

sudo pacman -S nvidia nvidia-settings nvidia-utils lib32-nvidia-utils lib32-opencl-nvidia opencl-nvidia libvdpau libxnvctrl vulkan-icd-loader lib32-vulkan-icd-loader

*** GAMING Config

***Gamemode is in the AUR run the following commands to install gamemode.
git clone https://aur.archlinux.org/gamemode.git && cd gamemode && makepkg -si && cd

same thing for 32bit gamemode.
git clone https://aur.archlinux.org/lib32-gamemode.git && cd lib32-gamemode && makepkg -si && cd

Now that it is installed we need to enable the service with this command
systemctl --user enable gamemoded && systemctl --user start gamemoded

To use gamemode for supertuxkart for example, run this terminal
gamemoderun supertuxkart

To use it in Steam edit the launch option for the desired game to
gamemoderun %command%

If gamemode does not run try to make it executable:
sudo chmod +x /usr/bin/gamemoderun

If gamemoderun does not work for you try this as a launch command:
LD_PRELOAD=$LD_PRELOAD:/usr/lib/x86_64-linux-gnu/libgamemodeauto.so.0 %command%

Create a Xorg Config file:
sudo nvidia-xconfig

Move it to the right directory:
sudo mv /etc/X11/xorg.conf /etc/X11/xorg.conf.d/20-nvidia.conf

Edit the file with the following command
sudo nano  /etc/X11/xorg.conf.d/20-nvidia.conf

Add in these lines under the "Device" section between the other options
Option         "TripleBuffer" "on"
Option         "Coolbits" "28"

Add in these lines under the "Screen" section between the other options.
Option         "metamodes" "nvidia-auto-select +0+0 {ForceCompositionPipeline=On, ForceFullCompositionPipeline=On}"
Option         "AllowIndirectGLXProtocol" "off"

Try this one with risk, It will be sure to crash GNOME, I am not sure about other DEs

just add it to the end of the file
Section "Extensions"
   Option         "Composite" "Disable"
EndSection

If you run into any problems, just hit CTRL ALT F3 to switch to a different tty login, run the command to edit the file again and put a # in front of the options that are giving you trouble and reboot

Alternatively you can just completely remove the file with the following command and reboot
sudo rm /etc/X11/xorg.conf.d/20-nvidia.conf

  
https://aur.archlinux.org/libstrangle-git.git
