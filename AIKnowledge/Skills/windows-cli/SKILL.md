---
name: "windows-cli"
description: "在 Windows 系统上执行命令行操作。Invoke when user needs to run Windows CMD, PowerShell commands, execute scripts, manage files, check system info, or perform any Windows CLI operations."
---

# Windows CLI MCP 技能

## 📋 技能概述

本技能用于在 Windows 系统上执行各种命令行操作，包括 PowerShell、CMD 命令执行、脚本运行、文件管理、系统信息查询等。

## 🎯 适用场景

- ✅ **执行 PowerShell 命令** - 系统管理、自动化任务
- ✅ **执行 CMD 命令** - 传统 Windows 命令
- ✅ **文件操作** - 复制、移动、删除、创建文件/文件夹
- ✅ **系统查询** - 查看系统信息、进程、服务
- ✅ **网络操作** - ping、tracert、netstat 等
- ✅ **软件安装** - 使用 winget、choco 等包管理器
- ✅ **注册表操作** - 查询、修改注册表
- ✅ **任务调度** - 创建、管理计划任务

## 🚫 禁止行为

- ❌ 执行需要管理员权限的操作（除非用户明确授权）
- ❌ 执行危险命令（如格式化磁盘、删除系统文件）
- ❌ 执行会修改系统关键配置的命令
- ❌ 执行会泄露敏感信息的命令

## 📊 命令执行流程

### 标准流程

```
1. 理解用户需求
   ↓
2. 分析命令安全性
   ↓
3. 选择合适的 Shell（PowerShell/CMD）
   ↓
4. 构建命令
   ↓
5. 执行命令
   ↓
6. 解析输出结果
   ↓
7. 返回结果给用户
```

### 安全性检查

在执行任何命令之前，必须进行安全性检查：

```typescript
// 危险命令检查列表
const dangerousCommands = [
  'format',      // 格式化磁盘
  'del /s',      // 删除所有文件
  'rd /s',       // 删除目录树
  'taskkill /f', // 强制结束进程
  'reg delete',  // 删除注册表项
  'shutdown',    // 关机
  'net user',    // 用户管理（可能需要权限）
];

// 检查命令是否安全
function isCommandSafe(command: string): boolean {
  // 检查是否包含危险命令
  // 检查是否需要管理员权限
  // 检查是否会影响系统稳定性
  return true; // 或 false
}
```

## 🔧 命令类型

### 1. 文件操作命令

#### PowerShell
```powershell
# 创建目录
New-Item -Path "C:\test" -ItemType Directory

# 复制文件
Copy-Item -Path "C:\source\file.txt" -Destination "C:\dest\"

# 移动文件
Move-Item -Path "C:\source\file.txt" -Destination "C:\dest\"

# 删除文件
Remove-Item -Path "C:\file.txt"

# 列出文件
Get-ChildItem -Path "C:\"

# 读取文件内容
Get-Content -Path "C:\file.txt"

# 写入文件
Set-Content -Path "C:\file.txt" -Value "内容"
```

#### CMD
```cmd
# 创建目录
mkdir C:\test

# 复制文件
copy C:\source\file.txt C:\dest\

# 移动文件
move C:\source\file.txt C:\dest\

# 删除文件
del C:\file.txt

# 列出文件
dir C:\

# 查看文件内容
type C:\file.txt
```

### 2. 系统查询命令

#### PowerShell
```powershell
# 查看系统信息
Get-ComputerInfo

# 查看进程
Get-Process

# 查看服务
Get-Service

# 查看磁盘空间
Get-PSDrive -PSProvider FileSystem

# 查看内存使用
Get-Counter "\Memory\Available MBytes"

# 查看 CPU 使用率
Get-Counter "\Processor(_Total)\% Processor Time"
```

#### CMD
```cmd
# 查看系统信息
systeminfo

# 查看进程
tasklist

# 查看服务
sc query

# 查看磁盘空间
wmic logicaldisk get size,freespace,caption

# 查看网络配置
ipconfig /all
```

### 3. 网络操作命令

```powershell
# Ping 测试
Test-Connection -ComputerName www.google.com -Count 4

# 端口扫描
Test-NetConnection -ComputerName www.example.com -Port 80

# DNS 查询
Resolve-DnsName -Name www.google.com

# 路由跟踪
tracert www.google.com

# 网络连接
netstat -an
```

### 4. 软件管理命令

#### Winget（Windows 包管理器）
```powershell
# 搜索软件
winget search vscode

# 安装软件
winget install Microsoft.VisualStudioCode

# 更新软件
winget upgrade Microsoft.VisualStudioCode

# 列出已安装软件
winget list
```

#### Chocolatey
```powershell
# 搜索软件
choco search vscode

# 安装软件
choco install vscode

# 更新软件
choco upgrade vscode

# 卸载软件
choco uninstall vscode
```

### 5. 注册表操作

```powershell
# 读取注册表
Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion"

# 创建注册表项
New-Item -Path "HKCU:\Software\MyApp" -Force

# 设置注册表值
Set-ItemProperty -Path "HKCU:\Software\MyApp" -Name "Setting" -Value "1"

# 删除注册表值
Remove-ItemProperty -Path "HKCU:\Software\MyApp" -Name "Setting"
```

## 📝 使用示例

### 示例 1：查询系统信息

**用户需求**：查看我的电脑配置

**执行命令**：
```powershell
Get-ComputerInfo | Select-Object CsName, OsName, OsArchitecture, TotalPhysicalMemory, CsProcessors
```

**输出结果**：
```
CsName          : DESKTOP-ABC123
OsName          : Microsoft Windows 11 Pro
OsArchitecture  : 64-bit
TotalPhysicalMemory : 16384 MB
CsProcessors    : Intel(R) Core(TM) i7-10700K CPU @ 3.80GHz
```

### 示例 2：管理文件

**用户需求**：在桌面创建一个测试文件夹并创建一个文件

**执行命令**：
```powershell
# 创建文件夹
New-Item -Path "$env:USERPROFILE\Desktop\TestFolder" -ItemType Directory

# 创建文件
Set-Content -Path "$env:USERPROFILE\Desktop\TestFolder\test.txt" -Value "这是一个测试文件"

# 验证
Get-ChildItem -Path "$env:USERPROFILE\Desktop\TestFolder"
```

### 示例 3：查看进程

**用户需求**：查看占用内存最多的前 5 个进程

**执行命令**：
```powershell
Get-Process | Sort-Object WorkingSet -Descending | Select-Object -First 5 Name, Id, WorkingSet, CPU
```

**输出结果**：
```
Name              Id      WorkingSet     CPU
----              --      ----------     ---
chrome          1234    524288000    15.2
code            5678    314572800     8.5
explorer        9012    157286400     3.1
```

### 示例 4：网络诊断

**用户需求**：检查网络连接

**执行命令**：
```powershell
# Ping 百度
Test-Connection -ComputerName www.baidu.com -Count 4

# 查看 IP 配置
ipconfig

# 查看 DNS
ipconfig /displaydns

# 查看网络连接
netstat -an | Select-String "ESTABLISHED"
```

## ⚠️ 安全注意事项

### 1. 权限检查

在执行命令前，检查是否需要管理员权限：

```powershell
# 检查是否为管理员
$isAdmin = ([Security.Principal.WindowsPrincipal] `
  [Security.Principal.WindowsIdentity]::GetCurrent()).`
  IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)

if (-not $isAdmin) {
  Write-Host "需要管理员权限" -ForegroundColor Red
  return
}
```

### 2. 危险命令拦截

以下命令需要特别小心，必须获得用户明确授权：

```typescript
const requiresExplicitConsent = [
  'Remove-Item -Recurse',  // 递归删除
  'Stop-Process -Force',   // 强制停止进程
  'Set-Service',           // 修改服务配置
  'New-LocalUser',         // 创建用户
  'Remove-LocalUser',      // 删除用户
];
```

### 3. 输出验证

执行命令后，验证输出是否合理：

```powershell
try {
  $result = Invoke-Expression $command
  if ($result -match "error|failed|access denied") {
    Write-Host "命令执行可能失败" -ForegroundColor Yellow
  }
  return $result
}
catch {
  Write-Host "命令执行失败：$($_.Exception.Message)" -ForegroundColor Red
  return $null
}
```

## 🎯 最佳实践

### 1. 使用 PowerShell 优先

```powershell
# ✅ 推荐：使用 PowerShell
Get-Process | Where-Object {$_.CPU -gt 100}

# ❌ 不推荐：使用 CMD
tasklist | findstr /C:"100"
```

### 2. 错误处理

```powershell
# 添加错误处理
try {
  $result = Invoke-Command -ScriptBlock {
    # 你的命令
  } -ErrorAction Stop
  
  return @{
    Success = $true
    Data = $result
  }
}
catch {
  return @{
    Success = $false
    Error = $_.Exception.Message
  }
}
```

### 3. 日志记录

```powershell
# 记录命令执行日志
$logFile = "C:\logs\command.log"
$logEntry = "$(Get-Date -Format 'yyyy-MM-dd HH:mm:ss') - $command"
Add-Content -Path $logFile -Value $logEntry
```

## 📚 常用命令速查

### 文件操作
| 操作 | PowerShell | CMD |
|------|-----------|-----|
| 创建目录 | `New-Item -Type Directory` | `mkdir` |
| 复制文件 | `Copy-Item` | `copy` |
| 移动文件 | `Move-Item` | `move` |
| 删除文件 | `Remove-Item` | `del` |
| 重命名 | `Rename-Item` | `ren` |

### 系统查询
| 操作 | PowerShell | CMD |
|------|-----------|-----|
| 系统信息 | `Get-ComputerInfo` | `systeminfo` |
| 进程列表 | `Get-Process` | `tasklist` |
| 服务列表 | `Get-Service` | `sc query` |
| 磁盘空间 | `Get-PSDrive` | `wmic logicaldisk` |
| 网络配置 | `Get-NetIPConfiguration` | `ipconfig` |

### 网络工具
| 操作 | 命令 |
|------|------|
| Ping | `Test-Connection` 或 `ping` |
| 端口测试 | `Test-NetConnection -Port` |
| DNS 查询 | `Resolve-DnsName` 或 `nslookup` |
| 路由跟踪 | `tracert` |
| 网络连接 | `netstat` |

## 🔍 故障排查

### 常见问题

#### 1. 权限不足
```
错误：Access is denied
解决：以管理员身份运行 PowerShell
```

#### 2. 命令不存在
```
错误：The term 'xxx' is not recognized
解决：安装相应模块或使用替代命令
```

#### 3. 路径错误
```
错误：Cannot find path
解决：检查路径是否正确，使用完整路径
```

## 📋 检查清单

在执行命令前，请确认：

- [ ] 命令是安全的，不会损害系统
- [ ] 已获得用户授权（特别是危险操作）
- [ ] 了解命令的作用和影响
- [ ] 有适当的错误处理
- [ ] 记录命令执行日志
- [ ] 验证输出结果合理性

---

**版本**: v1.0.0  
**创建日期**: 2026-03-27  
**维护者**: AI Assistant
