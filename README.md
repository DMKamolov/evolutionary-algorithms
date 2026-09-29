# DCS 340 · Optimization portfolio

My portfolio for the Introduction to Classical Methods in Optimization module of DCS 340 at Bates College: the class notebooks, my notes, and the investigations I built on top of them.

More about me: [diyorkamolov.me](https://diyorkamolov.me)

## About me as a learner

<!-- In your own voice, 3–5 sentences: how you learn best, what drew you to this module, and what you want this portfolio to show. -->
_add_

## Start here

| If you want to… | Open |
|---|---|
| See what we did in class | [Class notebooks](weeks/week-02-03-classic-optimization/class-code/) |
| Read the concepts in plain language | [Notes: classic optimization](weeks/week-02-03-classic-optimization/notes.md) |
| See my own investigations | [Playground notebook](weeks/week-02-03-classic-optimization/playground.ipynb) |
| See how I connect Colab, VS Code, Claude, Gemini, and GitHub | [WORKFLOW.md](WORKFLOW.md) |

## Weeks

| Week | Topic | Notes | Class code | Playground |
|---|---|---|---|---|
| 2–3 | Classic optimization: guess and check, bisection, gradient descent, Newton, Nelder–Mead | [notes](weeks/week-02-03-classic-optimization/notes.md) | [class-code](weeks/week-02-03-classic-optimization/class-code/) | [playground](weeks/week-02-03-classic-optimization/playground.ipynb) |

**Highlights so far**
- Found and verified three errors in the week 2–3 slides, including the wrong location for the 2D minimum ([errata](weeks/week-02-03-classic-optimization/notes.md#errata-things-on-the-slides-that-dont-check-out)).
- Showed exactly which learning rates make gradient descent converge, oscillate, or blow up, and why the answer is $\alpha < 2/\lambda_{\max}$.
- Raced bisection, gradient descent, and Newton on the same function: Newton hits 1e-10 accuracy in 5 steps; the others need 30–40.
- Worked through every "Try it yourself" challenge from the class notebooks, including a silent bug: change the terrain function and gradient descent keeps solving the old one. Fixed it with numerical derivatives.

## How I used generative AI

This module encourages using AI tools, so here is exactly how I used them.

- **Claude (Anthropic)** read the week 2–3 slides and both class notebooks and drafted the structure of this repo, the [notes](weeks/week-02-03-classic-optimization/notes.md), and the [playground](weeks/week-02-03-classic-optimization/playground.ipynb) investigations. <!-- Edit to describe what you reviewed, rewrote, or added. -->
- **Checking the class material:** Claude solved the slides' equations and re-ran the methods in code, which is how the three errata were found. <!-- Add how you double-checked them yourself, e.g. solving for the 2D minimum by hand. -->
- **Where the AI got it wrong:** in the first draft of the convergence race (playground section 7), bisection seemed to find the answer instantly. The chosen bracket happened to put the answer exactly on a midpoint, and the first fix did it again. Checking the output against expectations caught both; the final bracket makes that impossible. AI-generated results still need a sanity check.
- **Gemini in Colab:** <!-- describe how you used it -->_add_
- **My portfolio site:** <!-- describe how you used Claude / Claude Code to build diyorkamolov.me -->_add_

**What is mine:** the "My take" reflections in the playground, the self-study entries in the notes, and <!-- anything else you wrote or built yourself --> _add_.

## Repository layout

```
README.md
WORKFLOW.md                  how my tools connect to GitHub
weeks/
  week-02-03-classic-optimization/
    notes.md                 lecture notes, resources, errata
    class-code/              class Colab notebooks, unchanged
    playground.ipynb         my investigations
requirements.txt
```

## Running the notebooks

Each notebook runs top to bottom on its own, in Google Colab (File → Open notebook → GitHub) or locally:

```bash
pip install -r requirements.txt
jupyter notebook
```
