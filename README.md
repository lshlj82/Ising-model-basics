# The Ising Model, Interactively

An interactive, single-page web demo of the basics of the Ising model of a ferromagnet: the model itself, exact solutions for small systems and in one dimension, the mean-field approximation and spontaneous symmetry breaking, Monte Carlo simulation with the Metropolis algorithm, and a first look at correlations, critical points, and the renormalization group.

Created by **Claude Opus 5.5**, based on the lecture notes by **Sang Hoon Lee** (Chapter 8, Systems of Interacting Particles; Section 8.2, The Ising Model of a Ferromagnet). It completes the series of demos for Chapter 7 (the grand canonical ensemble, bosons and fermions, degenerate Fermi gases, blackbody radiation, the Debye theory of solids, and Bose–Einstein condensation).

## What's inside

**Ferromagnets.** Neighboring dipoles that prefer to align, the Curie temperature (about 1043 K for iron), domains, and why the Ising model describes a single domain with a preferred axis.

**The model.** s<sub>i</sub> = ±1, U = −ε Σ s<sub>i</sub>s<sub>j</sub> over neighboring pairs, and Z = Σ e<sup>−βU</sup> over all 2<sup>N</sup> states. A clickable 4 × 4 lattice marks each bond as parallel or antiparallel; its "Figure 8.4" preset reproduces Problem 8.15 (14 parallel, 10 antiparallel, U = −4ε). Because a 4 × 4 lattice has only 65,536 states, the demo also sums them all exactly to give ⟨U⟩, ⟨|M|⟩, the heat capacity, and the probability of the displayed state at any temperature.

**Two dipoles (Problem 8.17).** Z = 4 cosh βε, the probabilities of parallel and antiparallel alignment, U = −ε tanh βε, and the threshold T = 2ε/(k<sub>B</sub> ln 2) ≈ 2.885 ε/k<sub>B</sub> below which both-up beats one-up-one-down.

**The exact solution in one dimension (Problem 8.18).** Z = 2<sup>N</sup> cosh<sup>N−1</sup>(βε) and Ū = −Nε tanh βε, the analogy with the two-state paramagnet, and why there is no phase transition. A live 600-dipole chain runs the Metropolis algorithm, drawn as a space-time picture, with its measured energy compared with the exact value and the exact correlation length −1/ln tanh βε. The section also notes why s̄ = 0 by symmetry, leading to spontaneous symmetry breaking.

**The mean-field approximation.** s̄ = tanh(βεn s̄), solved graphically with stable and unstable solutions marked, k<sub>B</sub>T<sub>c</sub> = nε, and Problem 8.22's external field, with the region of the T–B plane that has three solutions. For Problem 8.24, the mean-field magnetization of the square lattice is compared with Onsager's exact result (T<sub>c</sub> = 4 vs. 2.269 ε/k<sub>B</sub>), including a log-log view near T<sub>c</sub> that shows the critical exponents β = 1/2 and 1/8, and the mean-field susceptibility diverging with γ = 1 on both sides.

**Monte Carlo simulation.** The Metropolis algorithm and detailed balance, running live on lattices from 45 × 45 to 270 × 270 with periodic boundaries, adjustable temperature and field, and running traces of energy and magnetization. A temperature scan, like the one in the lecture's Python code, measures the energy, magnetization, heat capacity, and susceptibility of a 24 × 24 lattice, with Onsager's exact magnetization for comparison.

**Correlations and scale invariance.** The correlation function c(r) = ⟨s<sub>i</sub>s<sub>j</sub>⟩ − s̄² of the live simulation (Problem 8.29) with its correlation length, and 3 × 3 majority-rule block-spin transformations, applied once and twice (Problem 8.32), with a short account of fixed points, universality, and the renormalization group.

## Running it

There is nothing to build or install. The whole demo is one self-contained file, `index.html`, with all CSS and JavaScript inline.

Open it locally by double-clicking `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Publishing with GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your main branch and the `/ (root)` folder, then save.
4. After a minute or so, the demo will be live at `https://<your-username>.github.io/<repository-name>/`.

## Technical notes

- Plain HTML, CSS, and vanilla JavaScript drawn on `<canvas>`. No frameworks, no build step.
- Temperatures are in units of ε/k<sub>B</sub>.
- The Monte Carlo engine is a standard single-flip Metropolis algorithm with a fast xorshift random-number generator and precomputed acceptance probabilities. Checked against Onsager's exact magnetization, it agrees to three digits below T<sub>c</sub> (for example 0.911 at T = 2 on a 48 × 48 lattice); the one-dimensional chain agrees with −tanh βε.
- The 4 × 4 lattice's exact thermodynamics come from a one-time enumeration of all 65,536 states, binned by energy and magnetization.
- The animations pause when scrolled off screen and start paused when the system asks for reduced motion.
- Equations are typeset with [MathJax 3](https://www.mathjax.org/) (SVG output, loaded from cdnjs), so they need no extra web fonts.
- The only other external resources are the Newsreader and Instrument Sans fonts from Google Fonts, with system font fallbacks if they fail to load.
- Opening the page requires an internet connection for MathJax; offline, the equations appear as raw TeX.
- Supports light and dark mode via `prefers-color-scheme`, and is responsive down to phone widths.

## Caveats

- Finite lattices only approximate the infinite system: above T<sub>c</sub> a small residual |M| remains, and the heat capacity and susceptibility show rounded peaks instead of true divergences.
- At low temperature a random start can get stuck in a long-lived metastable state with large domains, as the lecture notes.
- The correlation length in the clusters section is estimated from a single snapshot, so it fluctuates.

## Credits

- Demo: Claude Opus 5.5
- Physics content and examples: lecture notes by Sang Hoon Lee
- The lecture follows Daniel V. Schroeder, *An Introduction to Thermal Physics* (Section 8.2 and Problems 8.15, 8.17, 8.18, 8.22, 8.24, 8.29, and 8.32), and draws on N. Goldenfeld, *Lectures on Phase Transitions and the Renormalization Group*; M. E. J. Newman and G. T. Barkema, *Monte Carlo Methods in Statistical Physics*; and K. G. Wilson, "Problems in Physics with Many Scales of Length," *Scientific American* 241 (1979).

## License

No license has been chosen yet. Add a `LICENSE` file (for example, MIT or CC BY 4.0) before sharing or reusing this project publicly, and confirm that any use of the lecture material is permitted by its author.
