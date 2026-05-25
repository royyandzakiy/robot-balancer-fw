## done

- cpp23
- aem
- ble dfu (sysbuild mcuboot)
- rtt
- rename to: robot-balancer-fw
- tfm
- smf (fail, requires v3.2.x+)
- signed firmware

---

## todo

- tfm
- upgrade to 3.2.1
- smf (requires v3.2.x+)
- ztest + native_sim linux only (requires v3.2.x+)
- gtest (cmake fetch)

- fix: .vscode missing includes for zephyr/ncs
- west manifest
- devcontainer

---

- watchdog
- systemview (rtt-tracing) [link](https://docs.zephyrproject.org/latest/services/tracing/index.html)
- profiling ([perf](https://docs.zephyrproject.org/latest/services/profiling/perf.html))

---

- system design
- basic example: iotest: read mpu, read ble, set led pwm

---

- dts: led, mpu
- caf sensor mpu6050
- pwm led
- upgrade to 3.3.0+

---

- seperate core/ & app/
- create full template (generalize code)

---

- shell iotest-fw
- lvgl
