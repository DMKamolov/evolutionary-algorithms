# Weeks 2–3 · Classic optimization for finding min/max

**Source:** DCS 340 lecture slides, "Classic optimization methods: selected few" (18 slides). The opening slide frames these methods using a 2020 review in *H2Open Journal* on evolutionary and swarm algorithms in water resources engineering ([doi:10.2166/h2oj.2020.128](https://doi.org/10.2166/h2oj.2020.128)).

**Class code:** [`01-classic-optimization-1d`](class-code/01-classic-optimization-1d.ipynb) (a pumpkin fired from a cannon) and [`02-multivariable-optimization`](class-code/02-multivariable-optimization.ipynb) (a surveyor looking for the lowest point in a valley).

**Companion notebook:** [`playground.ipynb`](playground.ipynb) runs every method below from scratch, pushes each one until it breaks, and answers both class notebooks' "Try it yourself" challenges.

---

## The one idea behind all of it

Every method in this unit answers the same question: *where is the function flattest?* A smooth function's maximum or minimum sits where its derivative (or, in 2D, its gradient) is zero. The methods differ in **how much information about the function they use** to get there:

| Method | What it looks at | Dimensions |
|---|---|---|
| Guess and check | Function values only | Any |
| Nelder–Mead | Function values only, but moves a shape around | Any (small) |
| Bisection | Only the **sign** of $f'(x)$ | 1D |
| Gradient descent / ascent | The slope $f'(x)$ or gradient $\nabla f$ | Any |
| Newton's method | Slope **and** curvature ($f''$ or the Hessian $H$) | Any (small) |

More information per step means fewer steps, but each step costs more. That trade-off is the whole unit.

## The two running examples

- **1D:** $f(x) = 4 - (x-2)^2$, the height of a pumpkin at horizontal distance $x$. An upside-down parabola with its **maximum at $x = 2$**, where $f = 4$. Derivative $f'(x) = -2x + 4$, second derivative $f''(x) = -2$.
- **2D:** $g(x,y) = (x-2)^2 - xy + (y-3)^2$, the height of a surveyor's terrain. Gradient $\nabla g = \big(2x - y - 4,\ -x + 2y - 6\big)$. Setting both to zero gives the **minimum at $(14/3,\ 16/3) \approx (4.67,\ 5.33)$**. The Hessian is constant, $H = \begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix}$, with eigenvalues 1 and 3, so the surface is a stretched bowl.

---

## 1. Guess and check (random search)

Evaluate $f$ at a batch of points and keep the best one. No derivatives, no assumptions, works on anything. The catch: accuracy improves painfully slowly. In 1D, halving your error roughly doubles the number of points you need, and in higher dimensions it gets exponentially worse.

**Use it for:** a rough first look, or to pick starting points for a smarter method.

## 2. Bisection

Turn "find the max of $f$" into "find the root of $f'$". Start with an interval $[a, b]$ where $f'(a)$ and $f'(b)$ have opposite signs, so a zero must lie between them. Then repeat:

1. Take the midpoint $c = (a+b)/2$.
2. If $f'(c)$ has the same sign as $f'(a)$, the root is in $[c, b]$, so set $a = c$. Otherwise set $b = c$.
3. Stop when $|f'(c)|$ or the interval width is below a tolerance.

The interval halves every step, so after $n$ steps the uncertainty is $(b-a)/2^n$. That makes the number of steps **predictable in advance**: $n = \lceil \log_2((b-a)/\text{tol}) \rceil$.

On the running example with $[0, 3]$: midpoints go $1.5 \to 2.25 \to 1.875 \to \dots$, closing in on 2.

The class notebook calls bisection derivative-free. More precisely, it never needs the *size* of the slope, only its *sign*, but it does evaluate $f'$ at every midpoint. It also needs the bracket to leave room around the answer: in the notebook's pumpkin challenge, the new peak lands exactly on the bracket's edge, and bisection only just survives (see the playground, section 9).

- **Strengths:** guaranteed to converge once you have a valid bracket; needs only the sign of $f'$.
- **Weaknesses:** 1D only; you must find a bracket first; slow (one bit of precision per step).

## 3. Gradient descent (and ascent)

Stand somewhere, look at the slope, and step downhill (or uphill, to maximize). The step size is set by a **learning rate** $\alpha$:

- Minimize: $x_{n+1} = x_n - \alpha\, f'(x_n)$
- Maximize: $x_{n+1} = x_n + \alpha\, f'(x_n)$
- In 2D: $\mathbf{v}_{n+1} = \mathbf{v}_n - \alpha\, \nabla f(\mathbf{v}_n)$, updating both coordinates at once.

On the 1D example with $\alpha = 0.1$ from $x_0 = 0$, the guess creeps toward 2 (it reaches about 1.98 after 20 steps).

**Why $\alpha$ matters so much.** For the 1D parabola, the distance from the peak gets multiplied by $(1 - 2\alpha)$ every step. So:
- $0 < \alpha < 0.5$: smooth, steady approach.
- $\alpha = 0.5$: lands exactly on the peak in one step.
- $0.5 < \alpha < 1$: overshoots back and forth but still converges.
- $\alpha \ge 1$: bounces forever or blows up.

The class's 2D notebook runs 50 steps at $\alpha = 0.1$ and stops at $(4.64, 5.31)$: close, but not yet at $(4.67, 5.33)$.

In general, gradient descent on a bowl-shaped function is stable only if $\alpha < 2 / \lambda_{\max}$, where $\lambda_{\max}$ is the largest curvature (largest Hessian eigenvalue). For the 2D example that limit is $2/3$. The *smallest* curvature controls how slowly the last stretch goes, which is why 20 steps at $\alpha = 0.1$ still leave the 2D example well short of $(4.67, 5.33)$.

- **Strengths:** cheap per step; needs only first derivatives; scales to millions of dimensions (this is how neural networks are trained).
- **Weaknesses:** slow (linear) convergence; sensitive to $\alpha$; crawls on flat regions and long narrow valleys.

## 4. Newton's method

Use the curvature too. Approximate $f'$ near the current guess with its tangent line, $f'(x) \approx f'(x_n) + f''(x_n)(x - x_n)$, set that to zero, and solve for the next guess:

$$x_{n+1} = x_n - \frac{f'(x_n)}{f''(x_n)}$$

It's gradient descent where the step size is chosen automatically by the curvature: big steps where the function is flat, small steps where it bends sharply.

In 2D the second derivative becomes the Hessian matrix, and dividing becomes solving a linear system:

$$\mathbf{v}_{n+1} = \mathbf{v}_n - H^{-1}(\mathbf{v}_n)\, \nabla f(\mathbf{v}_n)$$

(In code, use `np.linalg.solve(H, g)` rather than actually inverting $H$.)

**On a quadratic, Newton is exact in one step**, because the tangent-line approximation of a linear $f'$ is perfect. For the 1D example, $x_1 = x_0 - (-2x_0 + 4)/(-2) = 2$ from any starting point. For the 2D example, one step from anywhere lands on $(14/3, 16/3)$.

- **Strengths:** very fast (quadratic) convergence near the answer, meaning the number of correct digits roughly doubles each step; no learning rate to tune.
- **Weaknesses:** needs second derivatives; breaks when $f'' = 0$; can diverge from a bad start; computing and solving with the Hessian gets expensive in high dimensions.
- **Subtle trap:** Newton finds *critical points*, not minima. It will happily converge to a maximum or a saddle point if that's the nearest place where the slope is zero.

## 5. Nelder–Mead (the simplex method)

A derivative-free method for 2+ dimensions. Keep a **simplex** (a triangle in 2D, a tetrahedron in 3D), rank its corners from best to worst, and improve the worst corner:

- **Reflect** it through the center of the other corners.
- **Expand** further if the reflection worked really well.
- **Contract** toward the best corner if it didn't.
- **Shrink** the whole shape if nothing works.

The triangle tumbles, stretches, and shrinks its way down into the valley. The class notebook frames it as the multi-dimensional cousin of bisection: both avoid slopes, relying on comparisons alone to shrink a region around the answer. In Python it's one line: `scipy.optimize.minimize(f, x0, method="Nelder-Mead")`.

- **Strengths:** no derivatives needed; robust on noisy or non-smooth functions.
- **Weaknesses:** slow; needs many function evaluations; unreliable beyond roughly 10 dimensions.

---

## Comparison

| | Bisection | Gradient descent | Newton | Nelder–Mead |
|---|---|---|---|---|
| Needs | Sign of $f'$, a bracket | $f'$ or $\nabla f$, a learning rate | $f'$ and $f''$ (or $H$) | Only $f$ |
| Speed | Linear (halves error) | Linear | Quadratic near the answer | Slow |
| Guaranteed? | Yes, with a bracket | Only if $\alpha$ is small enough | No | No |
| Scales to many dimensions? | No (1D only) | Yes | Poorly | Poorly |
| Reach for it when | 1D and you want certainty | High-dimensional, e.g. machine learning | Smooth, low-dimensional, need precision | No derivatives available |

---

## Resources

### Linked from the class slides

- **[Gradient Descent Unraveled](https://towardsdatascience.com/gradient-descent-unraveled-3274c895d12d)** (Towards Data Science). The slides' recommended deep dive on gradient descent.
- **[Newton's Method interactive graph](https://www.intmath.com/applications-differentiation/newtons-method-interactive.php)** (IntMath). Lets you drag the starting point and watch the tangent lines. Its fourth example, $f(x) = x^2$, shows the same slow convergence I found in [playground section 6](playground.ipynb).
- **Evolutionary algorithms, swarm intelligence methods, and their applications in water resources engineering** (*H2Open Journal*, 2020, [doi:10.2166/h2oj.2020.128](https://doi.org/10.2166/h2oj.2020.128)). The review the slides use to frame classical methods against newer ones.

### What I studied on my own

<!-- The rubric asks for evidence of videos, DataCamp, and math you studied to understand the material. Add real entries only. -->

| Resource | Type | What it helped me understand |
|---|---|---|
| _add_ | _video / DataCamp / article / textbook_ | _one or two sentences_ |

### Math this unit relies on

| Concept | Where it shows up | My notes |
|---|---|---|
| First-order Taylor expansion (tangent line) | Deriving Newton's update | _add_ |
| Partial derivatives and the gradient | Gradient descent in 2D | _add_ |
| The Hessian and its eigenvalues | Newton in 2D; why gradient descent needs $\alpha < 2/\lambda_{\max}$ | _add_ |

---

## Errata: things on the slides that don't check out

I verified these numerically in the [notebook](playground.ipynb) (section 1).

1. **The 2D minimum is at $(14/3, 16/3) \approx (4.67, 5.33)$, not $(2.33, 2.67)$.** The Nelder–Mead slide (8) and the 2D Newton slide (17) both state $(2.33, 2.67)$. Solving $\nabla g = 0$ gives $2x - y = 4$ and $-x + 2y = 6$, so $x = 14/3$ and $y = 16/3$. Running SciPy's Nelder–Mead also returns $(4.67, 5.33)$, and $g(4.67, 5.33) = -12.33$ is lower than $g(2.33, 2.67) = -6$. The 2D gradient descent slide (12) has the correct point, and so does the class's own multivariable notebook: its Nelder–Mead and Newton cells both print $(4.67, 5.33)$.
2. **Newton on $f(x) = 4 - (x-2)^2$ converges to $x = 2$, not $x = 0$.** Slide 15's own derivation ends with $x_{n+1} = 2$, but the conclusion line says $x = 0$.
3. **Slide 15's condition should read $f''(x) \neq 0$** (the "≠" symbol is missing).

---

## Open questions

<!-- Write your own. Some starters: -->
- How do libraries like PyTorch choose a learning rate, since picking $\alpha$ by hand is so fragile?
- Quasi-Newton methods (like BFGS) approximate the Hessian instead of computing it. How good is that approximation?
- The source paper is about *evolutionary* and *swarm* methods. When do those beat everything on this page?
