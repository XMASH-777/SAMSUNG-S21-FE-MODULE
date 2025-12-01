# INSTALL ROOT
```
pkg install tsu
```
# ขอสิทธิ์
```
tsu
```
# SHOE /#✅

# SAMSUNG-S21-FE-MODULE
```
cat > /sdcard/s21fe.sh << 'EOF'
# Samsung Galaxy S21 FE 5G - Core Props Spoof

# ใช้ resetprop เพื่อตั้งค่า System Properties (ต้องรันในโหมด Root)

# --- 1. Product & Device Identification ---
resetprop -n ro.product.model 'SM-G990B'
resetprop -n ro.product.brand 'samsung'
resetprop -n ro.product.name 'r9qxx'
resetprop -n ro.product.device 'r9q'
resetprop -n ro.product.manufacturer 'samsung'
resetprop -n ro.product.board 'lahaina' # เพิ่ม board name (Snapdragon 888)

# --- 2. Build Information ---
resetprop -n ro.build.product 'r9q'
resetprop -n ro.build.id 'TP1A.220624.014' # อ้างอิงจากรหัสบิวด์
resetprop -n ro.build.display.id 'TP1A.220624.014.G990BXXS6FWL2' # รหัสเต็ม
resetprop -n ro.build.version.release '13' # Android Version 13
resetprop -n ro.build.version.sdk '33' # API Level 33
resetprop -n ro.build.type 'user' # Build Type
resetprop -n ro.build.tags 'release-keys' # Build Tags

resetprop -n ro.build.fingerprint 'samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXS6FWL2:user/release-keys'

# --- 3. Hardware & Emulator Flags ---
resetprop -n ro.boot.hardware 'qcom'
resetprop -n ro.hardware 'qcom'
resetprop -n ro.soc.manufacturer 'Qualcomm' # เพิ่มผู้ผลิตชิป

# Disable Emulator flags (ป้องกันการตรวจจับว่าเป็นเครื่องจำลอง)
resetprop -n ro.kernel.qemu 0
resetprop -n ro.boot.qemu 0

echo '✔ Applied Samsung S21 FE core props'
EO
```
# NEXT 
```
sh /sdcard/s21fe.sh
```
# SHOW
✔ Applied Samsung S21 FE props
# CHECK
```
getprop ro.product.model
getprop ro.build.fingerprint
getprop ro.kernel.qemu
```
# ควรขื้น
SM-G990B
samsung/r9qxx/r9q:13/TP1A...
0
# CREATE MODULE 
```
mkdir -p /data/adb/service.d
cp /sdcard/s21fe.sh /data/adb/service.d/s21fe.sh
chmod 755 /data/adb/service.d/s21fe.sh
```
# ✅ ✅ CHECK 
```
getprop ro.product.model
```
# SHOW 
✅✅SM-G990B
# เพิ่มความเนียน
```
cat > /sdcard/s21fe_full.sh << 'EOF'
# Samsung Galaxy S21 FE 5G - Full Props Spoof (S21 FE, Unitel, Sensors)

# ใช้ resetprop เพื่อตั้งค่า System Properties (สคริปต์นี้ต้องรันในโหมด Root)

# --- 1. Product & Device Identification (S21 FE 5G) ---
resetprop -n ro.product.brand 'samsung'
resetprop -n ro.product.manufacturer 'samsung'
resetprop -n ro.product.model 'SM-G990B'
resetprop -n ro.product.device 'r9q'
resetprop -n ro.product.name 'r9qxx'
resetprop -n ro.product.board 'lahaina'

# --- 2. Build Information ---
resetprop -n ro.build.product 'r9q'
resetprop -n ro.build.id 'TP1A.220624.014'
resetprop -n ro.build.display.id 'TP1A.220624.014.G990BXXU6DWL2'
resetprop -n ro.build.version.release '13'
resetprop -n ro.build.version.sdk '33'
resetprop -n ro.build.version.security_patch '2024-01-01'
resetprop -n ro.build.type 'user'
resetprop -n ro.build.tags 'release-keys'
resetprop -n ro.build.fingerprint 'samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXU6DWL2:user/release-keys'

# Vendor Build
resetprop -n ro.vendor.build.fingerprint 'samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXU6DWL2:user/release-keys'
resetprop -n ro.vendor.product.device 'r9q'
resetprop -n ro.vendor.product.model 'SM-G990B'

# --- 3. Hardware & Emulator Flags ---
resetprop -n ro.hardware 'qcom'
resetprop -n ro.boot.hardware 'qcom'
resetprop -n ro.soc.manufacturer 'Qualcomm'
resetprop -n ro.soc.model 'Snapdragon 888'

# Disable Emulator flags
resetprop -n ro.kernel.qemu 0
resetprop -n ro.boot.qemu 0
resetprop -n ro.qemu.hw.mainkeys 1

# --- 4. Network Spoof: Unitel (Laos) ---
resetprop -n gsm.operator.numeric '45703'
resetprop -n gsm.sim.operator.numeric '45703'
resetprop -n gsm.operator.alpha 'Unitel'
resetprop -n gsm.sim.operator.alpha 'Unitel'
resetprop -n gsm.operator.iso-country 'la'
resetprop -n gsm.sim.operator.iso-country 'la'
resetprop -n gsm.network.type 'LTE'
resetprop -n gsm.operator.isroaming 'false'
resetprop -n gsm.sim.state 'LOADED'

# --- 5. Extra Props (Sensors, Display, Battery) ---
# Sensors
resetprop -n ro.hardware.sensors 'samsung_sensors'
resetprop -n ro.sensor.accelerometer 'Bosch BMA400'
resetprop -n ro.sensor.gyroscope 'Samsung Gyro'
resetprop -n ro.sensor.light 'LTR-559ALS Light Sensor'
resetprop -n ro.sensor.proximity 'Samsung Proximity'

# Battery
resetprop -n ro.product.battery.capacity '4500'
resetprop -n ro.product.battery.health 'Good'
resetprop -n ro.product.battery.technology 'Li-ion'

# Display
resetprop -n ro.sf.lcd_density '420'
resetprop -n ro.product.display.resolution '1080x2400'
resetprop -n ro.display.type 'AMOLED'
resetprop -n ro.product.display.size '6.4'
resetprop -n debug.sf.lcd_density '420'

echo '✔ S21 FE Full Props (including Unitel) Applied'
EOF
```
# RUNNING
```
sh /sdcard/s21fe_full.sh
```
✅✅✅
✔ S21 FE Extreme Props Applied

# RUN AUTOMATIC
```
cp /sdcard/s21fe_full.sh /data/adb/service.d/s21fe_full.sh
chmod 755 /data/adb/service.d/s21fe_full.sh
```
# NECK
```
getprop ro.product.model
getprop ro.build.fingerprint
getprop ro.kernel.qemu
```
# รีบูต✅✅✅
SM-G990B
samsung/r9qxx/r9q...
0
# FULL SCRIPT S21 SAFE 100 
```
cat > /sdcard/s21fe_extra.sh << 'EOF'
# Samsung Galaxy S21 FE 5G - Extra Identity Props Spoof

# ใช้ resetprop เพื่อตั้งค่า System Properties (สคริปต์นี้ต้องรันในโหมด Root)

# --- Sensors (เซ็นเซอร์) ---
resetprop -n ro.hardware.sensors 'samsung_sensors'
# ชื่อเซ็นเซอร์ที่สมจริงยิ่งขึ้นสำหรับ S21 FE (Snapdragon 888 Variant)
resetprop -n ro.sensor.accelerometer 'Bosch BMA400 Accelerometer'
resetprop -n ro.sensor.gyroscope 'Samsung Gyroscope Sensor'
resetprop -n ro.sensor.light 'LTR-559ALS Ambient Light Sensor'
resetprop -n ro.sensor.proximity 'Samsung Proximity Sensor'

# --- Battery (แบตเตอรี่) ---
resetprop -n ro.product.battery.capacity '4500'
resetprop -n ro.product.battery.health 'Good'
resetprop -n ro.product.battery.technology 'Li-ion'
resetprop -n ro.power_profile.battery.capacity '4500'
resetprop -n ro.battery.percentage '100'

# --- Display (หน้าจอ) ---
resetprop -n ro.sf.lcd_density '420'
resetprop -n ro.product.display.resolution '1080x2400'
resetprop -n ro.display.type 'AMOLED'
resetprop -n ro.product.display.size '6.4'
resetprop -n debug.sf.lcd_density '420'

# --- Radio / Modem ---
resetprop -n gsm.network.type 'LTE'
resetprop -n ro.radio.modem 'Qualcomm SDX55'
resetprop -n ro.vendor.radio.use-ppp 0
resetprop -n ro.telephony.default_network 33

# --- Confirm ---
echo '✔ Extra identity props applied (Sensors, Display, Battery, Modem)'
EOF
```

# ตากนั้น
```
sh /sdcard/s21fe_extra.sh
```
✅✅✅
# ✔ Extra identity props applied (Sensors, Display, Battery, Modem)

 # รันอัตโนมัติ
 ```
cp /sdcard/s21fe_extra.sh /data/adb/service.d/s21fe_extra.sh
chmod 755 /data/adb/service.d/s21fe_extra.sh
```

# ยืนยันอีกครัง เพื่อไมชนกับเครืองเดิม
```
resetprop ro.system_ext.build.fingerprint "samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXS6FWL2:user/release-keys"
```
# ทดสอบ
```
getprop ro.system_ext.build.fingerprint
```
# ต้องเป็นของ S21

# ป้องกันการ reset
```
nano /data/adb/service.d/fix_s21.sh
```
# ใส่คำสั่งนี้
```
#!/system/bin/sh
resetprop -n ro.system_ext.build.fingerprint "samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXS6FWL2:user/release-keys"
```
บันทึก
# CTRL + O = SAVE ENTER
ออก

# CTRL + X = EXIT
# CTRL + K = CLEAR

# บันทึกแล้วให้สิทธิ์
```
chmod 755 /data/adb/service.d/fix_s21.sh
```
# รันช้ำ
```
getprop ro.system_ext.build.fingerprint
```
# ถ้าขื้น Samsung แสดงว่า 100%

# NEXT MODULE 
```
# เข้า root ก่อน

# unify product/odm/product.vendor_dlkm/bootimage/vendor props -> S21 FE
resetprop -n ro.product.brand "samsung"
resetprop -n ro.product.manufacturer "samsung"
resetprop -n ro.product.model "SM-G990B"
resetprop -n ro.product.device "r9q"
resetprop -n ro.product.name "r9qxx"

resetprop -n ro.product.bootimage.brand "samsung"
resetprop -n ro.product.bootimage.device "r9q"
resetprop -n ro.product.bootimage.model "SM-G990B"
resetprop -n ro.product.bootimage.name "r9qxx"
resetprop -n ro.product.bootimage.manufacturer "samsung"

# odm / product / product.* (ที่ตกค้างเป็น OPPO ให้เป็น Samsung)
resetprop -n ro.product.odm.brand "samsung"
resetprop -n ro.product.odm.device "r9q"
resetprop -n ro.product.odm.manufacturer "samsung"
resetprop -n ro.product.odm.model "SM-G990B"
resetprop -n ro.product.odm.name "r9qxx"

resetprop -n ro.product.product.brand "samsung"
resetprop -n ro.product.product.device "r9q"
resetprop -n ro.product.product.manufacturer "samsung"
resetprop -n ro.product.product.model "SM-G990B"
resetprop -n ro.product.product.name "r9qxx"

# vendor_dlkm / vendor.* residues
resetprop -n ro.product.vendor.brand "samsung"
resetprop -n ro.product.vendor.device "r9q"
resetprop -n ro.product.vendor.manufacturer "samsung"
resetprop -n ro.product.vendor.model "SM-G990B"
resetprop -n ro.product.vendor.name "r9qxx"

resetprop -n ro.vendor_dlkm.build.fingerprint "samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXS6FWL2:user/release-keys"
resetprop -n ro.vendor.build.fingerprint "samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXS6FWL2:user/release-keys"
resetprop -n ro.system_ext.build.fingerprint "samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXS6FWL2:user/release-keys"

# clear any leftover emulator-ish props
resetprop -n ro.qemu.hw.mainkeys 0
resetprop -n ro.kernel.qemu 0
resetprop -n ro.boot.qemu 0
```
# CHECK ✅✅ 
```
getprop ro.build.fingerprint
getprop ro.vendor.build.fingerprint
getprop ro.odm.build.fingerprint
getprop ro.system_ext.build.fingerprint
getprop ro.vendor_dlkm.build.fingerprint

getprop ro.product.brand
getprop ro.product.manufacturer
getprop ro.product.model
getprop ro.product.device
getprop ro.product.name

getprop ro.product.odm.brand
getprop ro.product.odm.manufacturer
getprop ro.product.odm.model

getprop ro.product.product.brand
getprop ro.product.product.manufacturer
getprop ro.product.product.model

getprop ro.product.vendor.brand
getprop ro.product.vendor.manufacturer
getprop ro.product.vendor.model
```
# ควรเห็นค่า SAMSUMG/.....

# ทำให้ถาวร
```
mkdir -p /data/adb/service.d
cat > /data/adb/service.d/s21_unify.sh <<'EOF'
#!/system/bin/sh
# Re-apply S21FE unified props
resetprop -n ro.build.fingerprint "samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXS6FWL2:user/release-keys"
resetprop -n ro.vendor.build.fingerprint "samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXS6FWL2:user/release-keys"
resetprop -n ro.system_ext.build.fingerprint "samsung/r9qxx/r9q:13/TP1A.220624.014/G990BXXS6FWL2:user/release-keys"
# unify product/odm/vendor dlkm
resetprop -n ro.product.brand "samsung"
resetprop -n ro.product.manufacturer "samsung"
resetprop -n ro.product.model "SM-G990B"
resetprop -n ro.product.device "r9q"
resetprop -n ro.product.name "r9qxx"
resetprop -n ro.product.odm.brand "samsung"
resetprop -n ro.product.odm.manufacturer "samsung"
resetprop -n ro.product.odm.model "SM-G990B"
resetprop -n ro.product.product.brand "samsung"
resetprop -n ro.product.product.manufacturer "samsung"
resetprop -n ro.product.product.model "SM-G990B"
resetprop -n ro.product.vendor.brand "samsung"
resetprop -n ro.product.vendor.manufacturer "samsung"
resetprop -n ro.product.vendor.model "SM-G990B"
resetprop -n ro.qemu.hw.mainkeys 0
resetprop -n ro.kernel.qemu 0
resetprop -n ro.boot.qemu 0
EOF

chmod 755 /data/adb/service.d/s21_unify.sh
reboot
```
# CHECK EMULATOR SHOW 
```
getprop | grep -i qemu
```
