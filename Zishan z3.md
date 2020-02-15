# 紫珊 z3 降压

**修改电路将导致保修失效，严重则可能导致电路烧毁！！**

## 0x00 准备

为了缓解z3的发热问题，将原12v的运放供电降低至可接受的范围。分析电路可知电路中有两片SDB628负责供电，其中靠近USB接口的SDB628给运放OP275与LM4562供电，决定电压的两个电阻分别为：
<img src="https://latex.codecogs.com/gif.latex?R_{1}=100k\Omega, R_{2}=4.7k\Omega" />

根据芯片手册计算：
<img src="https://latex.codecogs.com/gif.latex?V_{out}=V_{ref}\times(1+R_{1}\div R_{2})=0.6V\times(1+100k\Omega\div4.7k\Omega)\approx13.3660V" />

<img src="https://latex.codecogs.com/gif.latex?
\frac{R_{1}}{R_{2}} =\frac{Vout}{0.6V} -1" />

查询手册可知OP275运放最低工作电压为4.5v，设降压后电压为6.5v，计算R1与R2比值
<img src="https://latex.codecogs.com/gif.latex?
\frac{R_{1}'}{R_{2}'} =\frac{Vout'}{0.6V} -1=\frac{6.5V}{0.6V} -1\approx9.83" />
取比值为10，设：
<img src="https://latex.codecogs.com/gif.latex?
R_{1}''=10k\Omega, R_{2}''=1k\Omega" />

<img src="https://latex.codecogs.com/gif.latex?
V_{out}''=0.6V\times(1+10k\Omega\div1k\Omega)=6.6V" />

输出电压满足预期。

## 0x01 替换电阻

tips1: z3用于粘贴电池的双面胶是一次性的，建议撕下后用洗板水清洗掉双面胶再继续。推荐3M的VHB胶带。

tips2: z3使用的贴片电阻为0805

**note: 注意检查电路防止虚焊，虚焊可能导致输出电压过高击穿运放**

![](https://github.com/smdll/some_md/blob/master/imgsrc/zishan_z3_circuit.jpg?raw=true)

## 0x02 参考

![IMG](https://img.alicdn.com/imgextra/i4/1654015063/TB2HO8IkgDD8KJjy0FdXXcjvXXa_!!1654015063.jpg)

http://www.ti.com/cn/lit/ds/symlink/lm4562.pdf

https://www.analog.com/media/en/technical-documentation/data-sheets/OP275.pdf

https://datasheet.lcsc.com/szlcsc/1809291616_SHOUDING-SDB628_C77805.pdf