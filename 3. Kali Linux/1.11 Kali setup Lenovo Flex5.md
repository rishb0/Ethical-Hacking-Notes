# **Kali Linux Setup Guide for Lenovo Flex 5 14ALC7**

This guide is for fresh Kali Linux installation with GNOME desktop on Lenovo IdeaPad Flex 5 14ALC7. Run these steps **before** applying the 125% scaling configuration.

## **1. Initial System Update**

**Update package lists and upgrade all packages to latest versions**
```bash
sudo apt update && sudo apt upgrade -y
```

**Install kernel headers for building drivers**
```bash
sudo apt install linux-headers-$(uname -r) -y
```

## **2. AMD Graphics Setup (Essential)**

**Install AMD graphics firmware for integrated Radeon graphics**
```bash
sudo apt install firmware-amd-graphics firmware-linux-nonfree -y
```

**Install hardware acceleration support**
```bash
sudo apt install mesa-vulkan-drivers libvulkan1 -y
```

## **3. Touchpad Configuration**

**Install modern touchpad driver**
```bash
sudo apt install xserver-xorg-input-libinput -y
```

**Create touchpad configuration for better gestures**
```bash
sudo mkdir -p /etc/X11/xorg.conf.d/
sudo nano /etc/X11/xorg.conf.d/30-touchpad.conf
```

Add this configuration:
```
Section "InputClass"
    Identifier "touchpad"
    Driver "libinput"
    MatchIsTouchpad "on"
    Option "Tapping" "on"
    Option "TappingButtonMap" "lrm"
    Option "NaturalScrolling" "on"
    Option "ScrollMethod" "twofinger"
    Option "ClickMethod" "clickfinger"
EndSection
```

## **4. WiFi & Bluetooth**

**Install WiFi firmware (covers most common chips)**
```bash
sudo apt install firmware-realtek firmware-atheros firmware-iwlwifi -y
```

**Install and enable Bluetooth**
```bash
sudo apt install blueman bluetooth -y
sudo systemctl enable bluetooth
sudo systemctl start bluetooth
```

## **5. Audio Configuration**

**Install audio packages and firmware**
```bash
sudo apt install pulseaudio pavucontrol alsa-utils -y
sudo apt install firmware-sof-signed -y
```

**Fix audio issues (if needed)**
```bash
echo "options snd-hda-intel model=auto" | sudo tee -a /etc/modprobe.d/alsa-base.conf
```

## **6. Webcam Support**

**Install webcam utilities**
```bash
sudo apt install v4l-utils cheese -y
```

## **7. Power Management**

**Install TLP for better battery life**
```bash
sudo apt install tlp tlp-rdw -y
sudo systemctl enable tlp
sudo systemctl start tlp
```

**Configure for better battery on AMD**
```bash
sudo nano /etc/tlp.conf
```

Add/modify these lines:
```
CPU_SCALING_GOVERNOR_ON_AC=performance
CPU_SCALING_GOVERNOR_ON_BAT=powersave
CPU_ENERGY_PERF_POLICY_ON_AC=performance
CPU_ENERGY_PERF_POLICY_ON_BAT=power
```

## **8. Essential Tools**

**Install useful system tools**
```bash
sudo apt install neofetch htop git curl wget build-essential -y
```

**Install multimedia codecs**
```bash
sudo apt install vlc ffmpeg gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly -y
```

## **9. GNOME Tweaks and Extensions**

**Install GNOME customization tools**
```bash
sudo apt install gnome-tweaks gnome-shell-extensions chrome-gnome-shell -y
```

## **10. Verify Hardware**

**Check graphics driver is loaded**
```bash
lspci -k | grep -A 3 -i vga
```
Should show: `Kernel driver in use: amdgpu`

**Test audio**
```bash
speaker-test -c 2 -t sine -f 1000
```
Press Ctrl+C to stop

**Test webcam**
```bash
cheese
```

**Check WiFi**
```bash
nmcli device wifi list
```

**Check battery status**
```bash
upower -i /org/freedesktop/UPower/devices/battery_BAT0
```

## **11. Reboot**

**Restart to ensure all drivers and services are loaded**
```bash
sudo reboot
```

## **Known Issues on This Model**

### **Not Working:**
- **Fingerprint reader** - No Linux drivers available for this model
- **Automatic screen rotation** - Sensors may not be fully supported

### **Partially Working:**
- **Touchscreen** - Basic touch works, but some gestures might not
- **Tablet mode detection** - Manual rotation only

### **Fully Working:**
- AMD Graphics ✓
- WiFi & Bluetooth ✓
- Touchpad with gestures ✓
- Audio (speakers & mic) ✓
- Webcam ✓
- Battery management ✓
- USB ports ✓
- HDMI output ✓

## **After This Setup**

Once you've completed these steps and rebooted, proceed with the **125% DPI scaling setup** guide to adjust the display size for the high-resolution 14" screen.

---

**Note:** This guide is specifically tested on Lenovo IdeaPad Flex 5 14ALC7 (Model 82R9) with Kali Linux 2024.x and GNOME desktop environment.

---
