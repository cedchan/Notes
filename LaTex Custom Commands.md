This document contains custom $\LaTeX$ commands that are used throughout this vault. The document must be in the vault for these commands to render correctly.

Note that in the tables below, the actual command definition is in the "Example" column.

## Math Commands
| Command              | Example                                                  | Notes                                                                          |
| -------------------- | -------------------------------------------------------- | ------------------------------------------------------------------------------ |
| `\E`                 | $\newcommand{\E}{\mathbb E}\E$                           |                                                                                |
| `\Var`               | $\newcommand{\Var}{{\rm Var}}\Var$                       |                                                                                |
| `\Cov`               | $\newcommand{\Cov}{{\rm Cov}}\Cov$                       |                                                                                |
| `\Corr`              | $\newcommand{\Corr}{{\rm Corr}}\Corr$                    |                                                                                |
| `\SD`                | $\newcommand{\SD}{{\rm SD}}\SD$                          |                                                                                |
| `\paren{[contents]}` | $\newcommand{\paren}[1]{\left(#1\right)}\paren{\frac12}$ | Automatic `\left` and `\right` placement for parentheses                       |
| `\qed`               | $$\newcommand{\qed}{\tag*{\(\square\)}}\qed$$            | Must be in `$$ $$` math mode. In `align` environment, must be preceded by `&`. |

## Statistics

| Command | Example                               | Notes                    |
| ------- | ------------------------------------- | ------------------------ |
| `\Expo` | $\newcommand{\Expo}{{\rm Expo}}\Expo$ | Exponential distribution |
| `\Unif` | $\newcommand{\Unif}{{\rm Unif}}\Unif$ | Uniform distribution     |
| `\N`    | $\newcommand{\N}{\mathcal N}\N$       | Normal distribution      |
| `\Bern` | $\newcommand{\Bern}{{\rm Bern}}\Bern$ | Bernoulli distribution   |
## Miscellaneous

| Command             | Example                                                                                       | Notes                                                                   |
| ------------------- | --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `\sc{[contents]}`   | $\newcommand{\sc}[1]{\firstchar#1\relax}\def\firstchar#1#2\relax{{\rm #1\small #2}}\sc{TEXT}$ | Only capitalizes first letter. All of `[contents]` must be capitalized. |
| `\lbr`              | $\newcommand{\lbr}{[\![}\lbr$                                                                 |                                                                         |
| `\rbr`1             | $\newcommand{\rbr}{]\!]}\rbr$                                                                 |                                                                         |
| `\sem{[contents]}`  | $\newcommand{\sem}[1]{\lbr #1\rbr}\sem{{\rm text}}$                                           | Semantic bracketing: `\lbr` and `\rbr` with `\left` and `\right`.       |
| `\bsem{[contents]}` | $\newcommand{bsem}[1]{\sem{\textbf{#1}}_s}\bsem{text}$                                        | `\sem` with bolding and supersecript $_s$.                              |
| `\Lbr`              | $\newcommand{\Lbr}{\Big[\!\!\Big[}\Lbr$                                                       | Large version of `\lbr`                                                 |
| `\Rbr`              | $\newcommand{\Rbr}{\Big]\!\!\Big]}\Rbr$                                                       | Large version of `\rbr`                                                 |
| `\Sem{[contents]}`  | $\newcommand{\Sem}[1]{\Lbr #1\Rbr}\Sem{\frac12}$                                              | Large version of `\se`                                                  |

