# ARCH LINUX 

## Inslling gnome extra themes

* sudo pacman -S gnome-extra-themes*

## delete orphans pakages 

                 sudo pacman -Rs $(pacman -Qtdq)


# video hardware aceleration

            sudo pacman -S libva-intel-driver intel-gpu-tools libva-utils*

## Firefox configuration:

<dl>
<dt>gfx.webrender.all           --) true</dt>  
<dt>media.ffmpeg.vaapi.enabled  --) true</dt>
<dt>media.ffvpx.enabled         --) false</dt>
<dt>media.rdd-vpx.enabled       --) false</dt>
<dt>media.av1.enabled           --) false</dt>
</dl>

##  X11:

      export MOZ_X11_EGL=1 && export MOZ_DISABLE_RDD_SANDBOX=1 && export MOZ_LOG="PlatformDecoderModule:5" && firefox*

## WAYLAND:
    
      export MOZ_ENABLE_WAYLAND=1 && export MOZ_DISABLE_RDD_SANDBOX=1 && export MOZ_LOG="PlatformDecoderModule:5" && firefox*



# Adding envirnment variables system wide:

    sudo nano /etc/environment

## Add the following line to /etc/environment
##  For X11:
        export MOZ_X11_EGL=1* 
        export MOZ_DISABLE_RDD_SANDBOX=1*


## For WAYLAND:

        export MOZ_ENABLE_WAYLAND=1*
        export MOZ_DISABLE_RDD_SANDBOX=1*
_____________________________________________________________
# INTEL DRIVERS

<dl>                   
<dt>sudo pacman -S intel-ucode</dt>
<dt>sudo grub-mkconfig -o /boot/grub/grub.cfg</dt>
</dl>

# Disable GRUB delay

- Add the following to /etc/default/grub:
 
### achieve the fastest possible boot:
     GRUB_FORCE_HIDDEN_MENU="true"

### Then put file 31_hold_shift to /etc/grub.d/.

Download 31_hold_shift (https://goo.gl/nac6Kp)

### Make it executable, and regenerate the grub configuration:

        sudo chmod a+x /etc/grub.d/31_hold_shift
        sudo grub-mkconfig -o /boot/grub/grub.cfg

# Set up firewall

<dl>
<dt>Install ufw:</dt>
<dt>sudo pacman -S ufw</dt>

<dt>Enable it.</dt>
<dt>sudo ufw enable </dt>

<dt>Check its status:</dt>
<dt>sudo ufw status verbose</dt>

<dt>Enable the start-up with the system:</dt>
<dt>sudo systemctl enable ufw.service</dt>
</dl>


# optimize pacman
- sudo pacman-optimize

# multilib enabling

-   sudo nano /etc/pacman.conf 

# discoment multilib

- sudo pacman -Syyuu


# nvidia setting

*sudo pacman -S nvidia nvidia-settings nvidia-utils lib32-nvidia-utils lib32-opencl-nvidia opencl-nvidia libvdpau libxnvctrl vulkan-icd-loader lib32-vulkan-icd-loader*

# GAMING Config

## Gamemode is in the AUR run the following commands to install gamemode.

<dl>
<dt>git clone https://aur.archlinux.org/gamemode.git && cd gamemode && makepkg -si && cd</dt>

  <dt>same thing for 32bit gamemode</dt>
<dt>git clone https://aur.archlinux.org/lib32-gamemode.git && cd lib32-gamemode && makepkg -si && cd</dt>

  <dt>Now that it is installed we need to enable the service with this command</dt>
<dt>systemctl --user enable gamemoded && systemctl --user start gamemoded</dt>

<dt>To use gamemode for supertuxkart for example, run this terminal
  gamemoderun supertuxkart</dt>

<dt>To use it in Steam edit the launch option for the desired game to
  gamemoderun %command%</dt>

<dt>If gamemode does not run try to make it executable:
sudo chmod +x /usr/bin/gamemoderun</dt>

<dt>If gamemoderun does not work for you try this as a launch command:
-LD_PRELOAD=$LD_PRELOAD:/usr/lib/x86_64-linux-gnu/libgamemodeauto.so.0 %command%</dt>
</dl>

> \` Create a Xorg Config file:
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
\`

  
https://aur.archlinux.org/libstrangle-git.git
