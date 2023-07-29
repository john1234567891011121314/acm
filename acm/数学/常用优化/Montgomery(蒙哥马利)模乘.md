## 蒙哥马利约减

# 看不懂

通常我们计算$xy \mod n$，我们需要$x*y-\lfloor \frac{x*y}{n} \rfloor  $

蒙哥马利模乘约减的思路是通过变换，将需要取模的数控制到很小的范围，最需要最多一次减法完成取模运算。通过选择除数为2的幂次，从而通过移位加快速度。

在竞赛范围(模数为正奇数)内，我们认为以下式子总会成立
$$
RR' \equiv 1 (\mod N)\\
RR' - NN' = 1\\
RR' - NN' \equiv 1 (\mod R) \\
-NN' \equiv 1 (\mod R) \\
0 < R' <N\\
0 <N'<R
$$
如果我们需要计算约减形式，即对于$T$我们想要求$TR'$
$$
T=T(RR'-NN')=TRR-TNN'\\
TR'=\frac{T+TNN'}{R}
$$
记$m=TN'$
$$
TR' \mod N \\
=\frac{T+mN}{R} \mod N \\
=\frac{T+(\lfloor \frac{T}{R} \rfloor R +(T\mod R))NN'}{R} \mod N \\
=\frac{T+(T\mod R)NN'}{R} +\lfloor \frac{T}{R} \rfloor NN' \mod N \\
=\frac{T+(T\mod R)NN'}{R}  \mod N \\
$$
