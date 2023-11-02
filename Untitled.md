
Journal of Phonetics: More theoretical
JASA: Acoustics
Journal of IPA: Language-specific

If you're familiar with some linear algebra: If $\vec c$ is the vector from the target's center to the fish's center and $\vec v$ is the velocity vector of the fish, then the reflection $\vec r$ is defined as $$\vec r = \vec v-2\cdot{\rm proj}_{\vec c}\vec v=\vec v-2\frac{\vec v\cdot\vec c}{\|\vec c\|^2}\vec c$$
If that didn't make sense to you, no worries. Try to follow this, where $v_x, v_y$ are `xVel`, `yVel` of the fish, respectively (note that the top value is the $x$ value of the vector and the bottom is the $y$): $$\vec c=\begin{bmatrix}x_{\rm fish}-x_{\rm target} \\ y_{\rm fish}-y_{\rm target}\end{bmatrix}=\begin{bmatrix}c_1 \\ c_2\end{bmatrix}, \vec v=\begin{bmatrix}v_x \\ v_y\end{bmatrix}$$
Then the above equation simplifies as follows: $$\begin{align*} \vec c_n&\triangleq\frac{\vec c}{\|\vec c\|^2}\\
&=\begin{bmatrix}\frac{c_1}{c_1^2+c_2^2} \\ \frac{c_2}{c_1^2+c_2^2}\end{bmatrix}\triangleq\begin{bmatrix}c_{n_1}\\ c_{n_2}\end{bmatrix}\\ \vec r&=\begin{bmatrix} v_x-2(v_xc_1+v_yc_2)c_{n_1} \\ v_y-2(v_xc_1+v_yc_2)c_{n_2} \\ \end{bmatrix} \end{align*}$$ Then the top value for $\vec r$ is your new `xVel` and the bottom is your new `yVel`.

