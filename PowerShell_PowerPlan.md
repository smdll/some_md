# PowerShell中设置电源计划

## 0x00 简介

平常开机处理一些事务的时候需要使用高性能电源计划，处理完的时候希望换成节能来省电。查找一些资料后决定编写一个PowerShell模块来完成这个工作。

## 0x01 细节

编写一个PowerShell模块，名为PowerPlan.psm1。内容如下：

```powershell
function Set-PowerPlan ($powerPlan) {
    try {
    	# For native language in English
    	# $powerPlan.toLower()
    	# $perf = powercfg -l | %{if($_.toLower().contains($powerPlan)) {$_.split()[3]}}
        # $currentPlan = $(powercfg -getactivescheme).split()[3]
        
    	# 适用于中文系统
        $perf = powercfg -l | %{if($_.contains($powerPlan)) {$_.split()[2]}}
        $currentPlan = $(powercfg -getactivescheme).split()[2]

        if ($currentPlan -ne $perf) {
            powercfg -setactive $perf
        }
    } catch {
    	#Write-Warning -Message "Unabled to set power plan to $powerPlan"
        Write-Warning -Message "无法设置电源计划为$powerPlan"
    }
}

function Set-PowerSaver {
	# Set-PowerPlan("power saver")
    Set-PowerPlan("节能")
}

function Set-PowerHighPerformance {
	# Set-PowerPlan("high performance")
    Set-PowerPlan("高性能")
}

function Set-PowerBalanced {
	# Set-PowerPlan("balanced")
    Set-PowerPlan("平衡")
}
```

保存至 `C:\Windows\System32\WindowsPowerShell\v1.0\Modules\PowerPlan\PowerPlan.psm1`

调用时首先

```powershell
 Import-Module PowerPlan
 Set-PowerSaver # 节能
 Set-PowerHighPerformance # 高性能
 Set-PowerBalanced # 平衡
 Set-PowerPlan "我的自定义计划1" # 自定义计划
```



## 0x02 参考

https://facility9.com/2015/07/controlling-the-windows-power-plan-with-powershell/