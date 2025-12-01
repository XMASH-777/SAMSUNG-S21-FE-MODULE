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
#### SHOW 
✅✅SM-G990B


