Command Prompt aliases (Linux-style, e.g., `ls` instead of `dir`)

Clone repo
`git clone https://github.com/nvth/cmd-aliases.git`

Quick setup (recommended)
1. Double-click `setup-aliases.bat`.

This will:
- Create `C:\alias\cmd.cmd` with only the `ls` alias.
- Import `autorun-hkcu.reg` so `cmd` auto-loads aliases.

Add more aliases
Edit `C:\alias\cmd.cmd` and add more `DOSKEY` lines.

Example `cmd.cmd`:
@echo off
DOSKEY ls=dir /B $*

Manual setup (optional)
1. Create `C:\alias\cmd.cmd` with your `DOSKEY` commands.
2. Import `autorun-hkcu.reg` (double-click), or:
   - Open Registry Editor (`regedit`).
   - Go to `HKEY_CURRENT_USER\Software\Microsoft\Command Processor`.
   - Add a String Value named `AutoRun` with value `C:\alias\cmd.cmd`.

Windows 10 / 11 (optional, system-wide)
Repeat the `AutoRun` value under:
`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor`

If you do not see `Command Processor`, create the key with that exact name.

Result

![poc](image.png)

Command reference (Linux style -> Windows CMD -> PowerShell)
| Linux        | Windows CMD       | PowerShell                          | Chức năng              |
| ------------ | ----------------- | ----------------------------------- | ---------------------- |
| `ls`         | `dir`             | `Get-ChildItem` (`ls`)              | Liệt kê file           |
| `pwd`        | `cd`              | `Get-Location`                      | Xem thư mục hiện tại   |
| `cd dir`     | `cd dir`          | `Set-Location dir`                  | Chuyển thư mục         |
| `mkdir test` | `mkdir test`      | `New-Item -ItemType Directory test` | Tạo thư mục            |
| `rmdir test` | `rmdir test`      | `Remove-Item test`                  | Xóa thư mục rỗng       |
| `rm file`    | `del file`        | `Remove-Item file`                  | Xóa file               |
| `rm -rf dir` | `rmdir /s /q dir` | `Remove-Item dir -Recurse -Force`   | Xóa thư mục có dữ liệu |
| `cp a b`     | `copy a b`        | `Copy-Item a b`                     | Copy file              |
| `cp -r a b`  | `xcopy a b /E`    | `Copy-Item a b -Recurse`            | Copy thư mục           |
| `mv a b`     | `move a b`        | `Move-Item a b`                     | Di chuyển / đổi tên    |
| `cat file`   | `type file`       | `Get-Content file`                  | Xem nội dung           |
| `less file`  | `more file`       | `Get-Content file -Wait`            | Xem từng trang         |
| `head -n 10 file` | -          | `Get-Content file -TotalCount 10`   | 10 dòng đầu            |
| `tail -n 10 file` | -          | `Get-Content file -Tail 10`         | 10 dòng cuối           |
| `tail -f log.txt` | -          | `Get-Content log.txt -Wait`         | Theo dõi log           |
| `grep "abc" file` | `findstr abc file` | `Select-String "abc" file`     | Tìm chuỗi              |
| `grep -R abc .`   | `findstr /S abc *` | `Select-String abc -Recurse .` | Tìm đệ quy             |
| `find . -name "*.txt"` | `dir /s *.txt` | `Get-ChildItem -Recurse -Filter *.txt` | Tìm file         |
| `wc -l file`      | -          | `(Get-Content file).Count`          | Đếm dòng              |
| `ps aux`   | `tasklist`          | `Get-Process`          | Xem process     |
| `kill PID` | `taskkill /PID PID` | `Stop-Process -Id PID` | Kill process    |
| `top`      | `taskmgr`           | `Get-Process | Sort CPU -Desc` | Monitor |
| `whoami`   | `whoami`            | `whoami`               | User hiện tại   |
| `id`       | -                   | `whoami /groups`       | Group           |
| `ip a`     | `ipconfig`          | `Get-NetIPAddress`     | Xem IP          |
| `ip r`     | `route print`       | `Get-NetRoute`         | Route           |
| `ping host` | `ping host`        | `Test-Connection host` | Ping            |
| `netstat -tunlp` | `netstat -ano` | `Get-NetTCPConnection` | Port            |
| `ss -lntp` | `netstat -ano`      | `Get-NetTCPConnection -State Listen` | Port listen |
| `curl url` | `curl url`          | `Invoke-WebRequest url` | HTTP request   |
| `wget url` | -                   | `Invoke-WebRequest url -OutFile a` | Download   |

Notes for aliases in `cmd.cmd`:
- `rm -rf` is aliased as `rmrf` (maps to `rmdir /S /Q`).
- `cp -r` is aliased as `cpr` (maps to `xcopy /E`).
- `cat` is aliased to `type`, and `less` is aliased to `more`.
- `grep` is aliased to `findstr`, `grepr` maps to recursive `findstr /S`, and `find` maps to `dir /s`.
- `ps` maps to `tasklist`, `kill` maps to `taskkill /PID`, and `top` maps to `taskmgr`.
- `ip` maps to `ipconfig`, `ipr` maps to `route print`, `ss` maps to `netstat -ano`, and `curl` maps to `curl`.
