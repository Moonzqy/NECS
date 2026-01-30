## 题目
- 请采用 PowerShell 脚本，实现对 Windows Server 系统性能信息的定时采集与日志记录，提高服务器运行状态监控与运维效率。
- 在Windows9中编写 C:\monitor.ps1 的 PowerShell 脚本，定义日志文件路径为C:\monitor\system_monitor.csv，获取当前系统时间，时间格式为：yyyy-MM-dd HH:mm:ss，采集服务器当前的 CPU 使用率（Processor(_Total)% Processor Time），采集服务器当前的可用内存大小（Memory\Available MBytes），将采集到的 时间、CPU 使用率、可用内存 按照 CSV 格式写入日志文件，若日志文件不存在，应自动创建，若存在，则以追加方式写入CPU 使用率与内存值均保留 两位小数。


## 解
```powershell
$LogFile = "C:\monitor\system_monitor.csv"

$Time = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
$CPU = (Get-Counter '\Processor(_Total)\% Processor Time').CounterSamples.CookedValue
$Memory = (Get-Counter '\Memory\Available MBytes').CounterSamples.CookedValue

"$Time,$([math]::Round($CPU,2)),$([math]::Round($Memory,2))" |
Out-File $LogFile -Append -Encoding UTF8

```