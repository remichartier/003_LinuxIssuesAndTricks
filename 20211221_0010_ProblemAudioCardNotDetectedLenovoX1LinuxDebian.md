# Problem X1 Carbon thinkpad Audio Dummy Output

- Machine : LE X1 CARBON V8 14 2020 (LIN) (NTB) US
  - X1 Carbon 6th Gen - (Type 20KH, 20KG) Laptop (ThinkPad) - Type 20KG

- Command used : 
```
Uname -r

Linux rchartier-xxxxx 5.10.46-5xxxxxx #1 SMP Debian 5.10.46-5xxxxx (2021-09-28) x86_64 GNU/Linux
```
```
lspci -nn | grep -i audio

00:1f.3 Audio device [0403]: Intel Corporation Sunrise Point-LP HD Audio [8086:9d71] (rev 21)
```

```pacmd list-cards

0 card(s) available.
```
```
pacmd list-sinks

1 sink(s) available.

  * index: 0

	name: <auto_null>

	driver: <module-null-sink.c>

	flags: DECIBEL_VOLUME LATENCY DYNAMIC_LATENCY

	state: IDLE

	suspend cause: (none)

	priority: 1000

	volume: front-left: 0 /   0% / -inf dB,   front-right: 65536 / 100% / 0.00 dB

	        balance 1.00

	base volume: 65536 / 100% / 0.00 dB

	volume steps: 65537

	muted: no

	current latency: 11.62 ms

	max request: 6 KiB

	max rewind: 6 KiB

	monitor source: 0

	sample spec: s16le 2ch 44100Hz

	channel map: front-left,front-right

	             Stereo

	used by: 0

	linked by: 1

	configured latency: 40.00 ms; range is 0.50 .. 2000.00 ms

	module: 13

	properties:

		device.description = "Dummy Output"

		device.class = "abstract"

		device.icon_name = "audio-card"
```
```
Lshw

sudo lshw|grep -i audio

             description: Audio device

             product: Sunrise Point-LP HD Audio

```

```
sudo dmesg | grep -i 'audio'
```
Gives nothing


```
Sudo lpci -v 

00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21) (prog-if 80)

	Subsystem: Lenovo Sunrise Point-LP HD Audio

	Flags: bus master, fast devsel, latency 64, IRQ 128, IOMMU group 9

	Memory at 2ffb028000 (64-bit, non-prefetchable) [size=16K]

-	Memory at 2ffb000000 (64-bit, non-prefetchable) [size=64K]

	Capabilities: [50] Power Management version 3

	Capabilities: [60] MSI: Enable+ Count=1/1 Maskable- 64bit+

	Kernel driver in use: snd_hda_intel

	Kernel modules: snd_hda_intel, snd_soc_skl
```


# Solution : 

I just found the solution on a blog (in french)

https://forum.ubuntu-fr.org/viewtopic.php?id=2049598

>> Problème réglé.

>> Je traduis la solution pour ceux que ça intérese :

>> Faire

>> sudo gedit /etc/default/grub

>> Remplacer GRUB_CMDLINE_LINUX_DEFAULT="quiet splash" par GRUB_CMDLINE_LINUX_DEFAULT="quiet splash snd_hda_intel.dmic_detect=0" et sauvegarder.

>> Ensuite faire :

>> sudo update-grub

>> et redémarer.

# Translation : 

- `sudo gedit /etc/default/grub`

- Replace `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"` with `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash snd_hda_intel.dmic_detect=0"` and save.

- Then `sudo update-grub`

- And then re-start computer.
