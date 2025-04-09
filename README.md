# dell-xps-9510
Linux set up for the Dell XPS 9510

After a long time trying to get the Dell XPS 9510 (OLED 3.5K) i7 to work various flavours of Linux I eventually managed to get it working with my day to day work distro which is Manjaro.

However, after installing some software (no idea what it was), it never booted again so wiped it and tried various different distros all with the same problem - the dreaded black/blank screen.  In the end I tried ZorinOS with Nvidia and it worked straight away, then once I installed it I was back to the dreaded black screen.  After many hours it seems it was down to the "preferred" Nvidia drivers (535) not actually working.  I switched to "550" and wrked straight away, but was a little slow in booting initially.

Once it was booted it was fine.

If you can get into the GRUB menu (Esc at the Dell logo), highlight Zorin and click "e" to edit the grub item, then remove "splash" and "quiet" and add "nomodeset", this shoudl evenbtually get you into the GUI.

Next go into "software" and "additional" and change the NVidia drivers to 550 and once done reboot.

Be patient, it takes quite some time to boot into the GUI. (5m36s)

Once you have logged in it will go black again for a short time and then you'll be at the desktop.

Run "systemd-analyze" to check the time it takes to get to the GUI.

If the time is too long it may be down to waiting for the network and you can disbale the wait intil network is available by typing:

"sudo systemctl disable NetworkManager-wait-online.service"

Still too slow for so I ran "systemd-analyze blame" to see what is taking so long in the boot process.  You also run "systemd-analyze critical-chain" to get the chained events.

Now under two minutes which is still slow, so changed "Fast boot" from "Thourough" to "Auto" which made things worse, so reverted back.

Will stick with ~2 minutes, once booted and logged in it runs lovely.

After a couple of reboots over a span of a week, log in time is now much better.

**Edit:** Have now moved to Fedora and apart from a black screen at startup (which was fixed by using nomodeset in Grub), its very quick to boot.  If you're sticking with Manjaro (which I have with my workstation), trying the nomodeset in Grub may well fix the long boot time as its probably booted fine but you can't see it.

**Edit (2):** Laptop had a faulty motherboard/screen - had both replaced under warranty and no issues since, no need for nomodeset
