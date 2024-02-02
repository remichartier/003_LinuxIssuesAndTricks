# Remote Desktop Control solutions on different OS and Sleep / Wakeup functionalities

Those solutions are not exhaustive, it is just a list of Desktop Remote Control solutions I walked through in my professional life.

## ChromeOS
- Chrome Remote Desktop (CRD) (Google ChromeOS solution)

## Windows 10
- Remote Desktop Connection (Microsoft solution)

## Linux Ubuntu 18.04, 20.04
- NoMachine

## Sleep / Wakeup functionalities

Sources:
- Windows:
  - https://www.energystar.gov/products/low_carbon_it_campaign/business_case/24_7_remote_access
  - https://helpdesk.flexradio.com/hc/en-us/articles/202118518-Optimizing-Ethernet-Adapter-Settings-for-Maximum-Performance
  - https://techgenix.com/advanced-network-adapter-driver-settings/ --> ARP Offload ("ARP Proxy") and NS Offload

- Linux Ubuntu NoMachine:
  - https://forums.nomachine.com/topic/wake-on-lan-by-ip-address

- Tricks to wakeup remote computers from Sleep/Suspend modes (prevent having to keep computers switched on 24/7 and 99% of their time in idle --> save power/energy/electric grid/$s)
  - Windows 10 / Microsoft Remote Desktop Connection:
    - Possible to wakeup from Sleep using Remote Desktop Connection if PC Network Card supports ARP Offload and NS Offload and if they are activated (Device Manager/Network Cards/Ethernet/properties)
  - Linux Ubuntu / NoMachine:
    - Possible to wakeup from Suspend mode using NoMachine if BIOS/UEFI Network WakeOnLan (WoL) enabled, + if WoL enabled on NoMachine Server settings on remote computer + if network router allows WoL packets to pass through the network.
