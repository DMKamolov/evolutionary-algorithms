# DCS 340 · Optimization portfolio

My portfolio for the Introduction to Classical Methods in Optimization module of DCS 340 at Bates College: the class notebooks, my notes, and the investigations I built on top of them.

More about me: [diyorkamolov.me](https://diyorkamolov.me)

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

## How I used generative AI

This module encourages using AI tools, so here is exactly how I used them.

- **Claude (Anthropic)** read the week 2–3 slides and both class notebooks and drafted the structure of this repo, for visualization of plots, learning more about specific math problems, and understanding what methods do step by step. I also used Claude Code to refine my website and repo structure. 

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
