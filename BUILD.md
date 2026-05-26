# Getting Started

All the below setups has successfully been built using ncs `v3.3.0` in win11

## Build Normally

```bash
west build --build-dir c:/project-coding/iot/projects/balancer-robot-fw/build c:/project-coding/iot/projects/balancer-robot-fw --pristine --board nrf5340dk/nrf5340/cpuapp -- -DEXTRA_CONF_FILE="debug-overlay.conf" -DDEBUG_THREAD_INFO=Off -Dbalancer-robot-fw_DEBUG_THREAD_INFO=On -Dmcuboot_DEBUG_THREAD_INFO=Off
```

## Build TFM

- Bash command

```bash
west build --build-dir c:/project-coding/iot/projects/balancer-robot-fw/build_v330_ns c:/project-coding/iot/projects/balancer-robot-fw --pristine --board nrf5340dk/nrf5340/cpuapp/ns -- -DEXTRA_CONF_FILE="debug-overlay.conf;tfm-overlay.conf" -DDEBUG_THREAD_INFO=On -DCONFIG_DEBUG_THREAD_INFO=y -Dbalancer-robot-fw_DEBUG_THREAD_INFO=On -Dmcuboot_DEBUG_THREAD_INFO=Off
```

- Result

```bash
...

-- Configuring done (1.9s)
-- Generating done (0.2s)
-- Build files have been written to: C:/project-coding/iot/projects/balancer-robot-fw/build_v330_ns/balancer-robot-fw/tfm
[162/168] Linking C executable bin\tfm_s.axf
Memory region         Used Size  Region Size  %age Used
           FLASH:       64396 B      65024 B     99.03%
             RAM:       14724 B        32 KB     44.93%
[17/390] Performing install step for 'tfm'
-- Install configuration: "Debug"
----- Installing platform NS -----
[389/390] Linking CXX executable zephyr\zephyr.elf
Memory region         Used Size  Region Size  %age Used
           FLASH:      188984 B       416 KB     44.36%
             RAM:       88660 B       416 KB     20.81%
        IDT_LIST:          0 GB        32 KB      0.00%
Generating files from C:/project-coding/iot/projects/balancer-robot-fw/build_v330_ns/balancer-robot-fw/zephyr/zephyr.elf for board: nrf5340dk/nrf5340/cpuapp/ns
image.py: sign the payload
image.py: sign the payload
[6/201] Generating include/generated/zephyr/version.h
-- Zephyr version: 4.3.99 (C:/ncs/v3.3.0/zephyr), build: ncs-v3.3.0
[201/201] Linking C executable zephyr\zephyr.elf
Memory region         Used Size  Region Size  %age Used
           FLASH:       35600 B        48 KB     72.43%
             RAM:       16720 B        32 KB     51.03%
        IDT_LIST:          0 GB        32 KB      0.00%
Generating files from C:/project-coding/iot/projects/balancer-robot-fw/build_v330_ns/mcuboot/zephyr/zephyr.elf for board: nrf5340dk/nrf5340/cpuapp
[20/20] Generating ../merged.hex
```

## DFU BLE

- Use nrf connect app
- Scan then connect to it
- Select DFU button on the top right
- Select `zephyr.signed.bin` file
- Will start uploading
  - Will succeed if properly signed, or if is also `_ns`

```bash
# copy to phone
balancer-robot-fw\build\balancer-robot-fw\zephyr\zephyr.signed.bin
```

![ble-connected](docs/ble-connected.png)
![ble-smp-dfu](docs/ble-smp-dfu.png)

## Sign Key

Create signing_key, this is a secret, do NOT push it into repo. Ensure the key type generated with imgtool is the same signature type set in sysbuild

```bash
imgtool keygen -k signing_key.pem -t ecdsa-p256
```

```bash
# add to sysbuild.conf
SB_CONFIG_BOOT_SIGNATURE_KEY_FILE="C:/project-coding/iot/projects/balancer-robot-fw/signing_key.pem"
SB_CONFIG_BOOT_SIGNATURE_TYPE_ECDSA_P256=y
```
