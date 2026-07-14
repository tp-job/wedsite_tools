See also: [[building a Frontend]] · [[building a Backend]] · [[building a Flutter]] · [[Web Tools MOC]] · [[Support Tools]]

### Dev workflow

```cmd
cd client && npm run dev
cd server && npm run dev
```

### Network / Connectivity

```cmd
curl ascii.live/can-you-hear-me

ipconfig
ipconfig /all
ipconfig /flushdns
ipconfig /release
ipconfig /renew

ping google.com -t
tracert google.com
nslookup google.com

netstat -ano | findstr LISTENING
netstat -ano | findstr :3000

hostname
net session
net use
```

### Process management (find & kill port)

```cmd
:: หา process ที่ใช้ port ค้างอยู่ เช่น 3000
netstat -ano | findstr :3000

:: kill process ด้วย PID
taskkill /PID <pid> /F

:: kill ตามชื่อ process
taskkill /IM node.exe /F

:: list process ทั้งหมด
tasklist
tasklist | findstr node
```

### System diagnostics & repair

```cmd
sfc /scannow
DISM /Online /Cleanup-Image /RestoreHealth
DISM /Online /Cleanup-Image /ScanHealth
chkdsk C: /f /r

:: system info
systeminfo
wmic cpu get name
wmic memorychip get capacity
wmic diskdrive get model,size

:: uptime
net statistics workstation
```

### File / Folder operations

```cmd
:: ลบโฟลเดอร์แบบไม่ถาม (silent, recursive)
rmdir /s /q foldername

:: ลบไฟล์ทั้งหมดใน folder รวม subfolder
del /s /q foldername\*

:: copy โฟลเดอร์ทั้งหมด (รวม subfolder + attributes)
xcopy source destination /E /H /C /I

:: sync สอง folder (robust copy)
robocopy source destination /MIR

:: สร้างไฟล์ว่าง
type nul > filename.txt

:: หาไฟล์ตามชื่อ/นามสกุลทั้งไดรฟ์
dir /s /b *.env
where /r C:\Projects *.log
```

### Disk & storage

```cmd
:: พื้นที่ดิสก์คงเหลือ
wmic logicaldisk get size,freespace,caption

:: cleanup
cleanmgr /d C:

:: disk usage ของ folder (ต้องใช้ PowerShell)
powershell "Get-ChildItem -Recurse | Measure-Object -Property Length -Sum"
```

### Environment Variables

```cmd
:: ดูค่า env var
echo %PATH%
set

:: ตั้งค่า env var แบบถาวร (user scope)
setx API_KEY "your-value"

:: ตั้งค่าแบบชั่วคราว (session เดียว)
set API_KEY=your-value
```

### Node.js / npm / package managers

```cmd
node -v
npm -v

:: ล้าง cache เวลา install แปลกๆ
npm cache clean --force

:: ลบ node_modules + lock แล้วลงใหม่ (Windows ไม่มี rm -rf)
rmdir /s /q node_modules
del package-lock.json
npm install

:: เช็ค package ที่ล้าสมัย / เปลี่ยนเวอร์ชัน
npm outdated
npm update

:: run script เฉพาะ workspace (monorepo)
npm run dev --workspace=client

:: global packages ที่ลงไว้
npm list -g --depth=0
```

### Git (ที่ใช้บ่อยแต่ลืมบ่อย)

```cmd
:: ดู remote + branch
git remote -v
git branch -a

:: ยกเลิก commit ล่าสุดแต่เก็บไฟล์ไว้ (unstage)
git reset --soft HEAD~1

:: ทิ้ง local changes ทั้งหมด (ระวัง: ทำลายงานที่ยังไม่ commit)
git reset --hard HEAD
git clean -fd

:: ดู log แบบ graph สวยๆ
git log --oneline --graph --all --decorate

:: แก้ commit message ล่าสุด (ยังไม่ push)
git commit --amend -m "new message"

:: stash งานที่ทำค้างไว้
git stash
git stash pop
git stash list

:: sync fork กับ upstream
git fetch upstream
git merge upstream/main
```

### Windows services

```cmd
:: list service ทั้งหมด
sc query

:: start / stop / restart service
net start "ServiceName"
net stop "ServiceName"

:: เช็ค service ที่รันอยู่แบบกรอง
sc query state= all | findstr /i "mongodb"
```

### Firewall & ports

```cmd
:: เปิด port ผ่าน firewall
netsh advfirewall firewall add rule name="Open Port 3000" dir=in action=allow protocol=TCP localport=3000

:: ดู rule ทั้งหมด
netsh advfirewall firewall show rule name=all
```

### Scheduled tasks / automation

```cmd
:: list scheduled task
schtasks /query /fo LIST /v

:: สร้าง task รันทุกวัน
schtasks /create /sc daily /tn "MyTask" /tr "C:\path\to\script.bat" /st 09:00
```

### Misc / Quality of life

```cmd
:: เปิด explorer จาก terminal ตำแหน่งปัจจุบัน
start .

:: เปิดไฟล์ด้วย default app
start filename.pdf

:: copy path ปัจจุบันไปยัง clipboard
cd | clip

:: comparing สอง text file
fc file1.txt file2.txt

:: เปิด VSCode ที่ folder ปัจจุบัน
code .
```

===ทุกคำสั่งให้เปิด tab ใหม่===
