# Newton's algo

for normal `fast_sqrt`

$$
\begin{align}
 & f(x) = x^{2} = \mathrm{Num}\\
 & \mathrm{trial\ root :} x^{\mathrm{trial}} \\
 & x^{\mathrm{next}} = x^{\mathrm{trial}} - \frac{(x^{\mathrm{trial}})^{2}-\mathrm{Num}} {2x^{\mathrm{trial}}}
\end{align}
$$
for countdown `fast_sqrtcountdown`
$$
\begin{align}
 & f(x) = \frac{1}{x^{2}} = \mathrm{Num} \\
 & \mathrm{trial\  root:} x^{\mathrm{trial}}  \\
 & x^{\mathrm{next}} = x^{\mathrm{trial}} - \frac{\left( \frac{1}{(x^{\mathrm{trial}})^{2}}-\mathrm{Num} \right)}{-2 \left( \frac{1}{x^{\mathrm{trial}}} \right)^{3}} = x^{\mathrm{trial}} - \frac{\mathrm{Num}\times (x^{\mathrm{trial}})^{3} - x^{\mathrm{trial}}}{2}  \\
 &  \ \ \ \ \ \ \ \ = x^{\mathrm{trial}}\left(1.5- \frac{\mathrm{Num}\times(x^{\mathrm{trial}})^{2}}{2}   \right) 
\end{align}
$$
