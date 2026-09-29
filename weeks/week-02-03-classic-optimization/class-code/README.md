# Class code · weeks 2–3

The notebooks we ran in class, saved unchanged. My own experiments live one folder up in [`playground.ipynb`](../playground.ipynb), so it's always clear what came from class and what I built.

| Notebook | What it covers |
|---|---|
| [`01-classic-optimization-1d.ipynb`](01-classic-optimization-1d.ipynb) | Finding the peak of a pumpkin's flight, $f(x) = 4 - (x-2)^2$: guess and check, gradient ascent, bisection, and Newton's method |
| [`02-multivariable-optimization.ipynb`](02-multivariable-optimization.ipynb) | Finding the lowest point of a surveyor's terrain, $f(x,y) = (x-2)^2 - xy + (y-3)^2$: Nelder–Mead, gradient descent, and Newton's method with the Hessian |

Both "Try it yourself" sections at the end of these notebooks are worked through in [playground section 9](../playground.ipynb).

## How to add a Colab notebook here

**Option A: straight from Colab (no download)**
1. Open the notebook in Colab.
2. **File → Save a copy in GitHub**.
3. Authorize GitHub if asked, pick this repository and branch, and set the file path to
   `weeks/week-02-03-classic-optimization/class-code/01-short-name.ipynb`.
4. Leave "Include a link to Colaboratory" checked. It adds an "Open in Colab" badge to the notebook.

**Option B: download and commit**
1. In Colab: **File → Download → Download .ipynb**.
2. Rename it (e.g. `01-bisection-and-gradient-descent.ipynb`) and move it into this folder.
3. Commit and push.

Before saving, run **Runtime → Run all** so the outputs and plots are stored in the file; GitHub displays them without anyone needing to run the code.
