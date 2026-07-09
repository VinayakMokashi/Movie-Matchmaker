# 🎬 Movie Matchmaker

![Python](https://img.shields.io/badge/Python-3.9-blue.svg)
![pandas](https://img.shields.io/badge/pandas-data-150458.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-notebook-orange.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

An **item-based collaborative-filtering** movie recommender built on the
[MovieLens 100K](https://grouplens.org/datasets/movielens/100k/) dataset. It
learns how movies "move together" across thousands of users' ratings and
recommends the films most correlated with the ones you already like — and, as a
personal twist, it finishes by recommending movies for **me**, based on my own
ratings.

> No machine-learning framework needed — the whole engine is a ratings matrix and
> a correlation, in pure pandas.

---

## Table of Contents

- [How it works](#how-it-works)
- [Dataset](#dataset)
- [Results](#results)
- [Repository structure](#repository-structure)
- [How to run](#how-to-run)
- [Future work](#future-work)
- [License](#license)

---

## How it works

There are two flavours of collaborative filtering:

- **User-based** — find users similar to you and recommend what *they* liked.
  Problem: there are far more users than items, similarity is expensive at scale,
  and people's taste drifts over time.
- **Item-based** — find items similar to the ones you liked. Items have stable
  characteristics, so item-to-item similarity is cheaper and holds up over time.

This project uses the **item-based** approach:

1. **Build a user × movie matrix** — one row per user, one column per movie,
   cells holding ratings (mostly empty, since nobody rates everything).
2. **Correlate movies** — two movies are "similar" if the same users tend to rate
   them alike (Pearson correlation across the shared raters).
3. **Guard against noise** — only trust correlations backed by a minimum number
   of shared ratings (`min_periods = 80`); a movie with one 5-star review isn't a
   reliable recommendation.
4. **Recommend** — for a target movie, return its most-correlated neighbours; for
   a *person*, scale each movie's correlations by the ratings that person gave and
   sum them into a personalized ranking.

## Dataset

[MovieLens 100K](https://grouplens.org/datasets/movielens/100k/) — 100,000
ratings from 943 users on 1,682 movies.

| File | What it holds |
| --- | --- |
| `u.data` | Raw ratings: `user_id`, `item_id`, `rating`, `timestamp` (tab-separated) |
| `Movie_Id_Titles` | Lookup table mapping `item_id` → movie title |
| `My_Ratings.csv` | A few movies I rated myself — the seed for my personal recommendations |

> I also added myself to `u.data` as **user 0** (a handful of my own ratings), so
> my taste is part of the similarity matrix, not just an afterthought.

## Results

**Movies similar to _Titanic (1997)_** (≥ 80 shared ratings):

| Movie | Correlation |
| --- | :---: |
| The River Wild (1994) | 0.50 |
| The Abyss (1989) | 0.47 |
| Bram Stoker's Dracula (1992) | 0.44 |
| True Lies (1994) | 0.44 |

**My personalized top picks** (driven mostly by _Liar Liar (1997)_, my highest
rating):

`Con Air` · `Pretty Woman` · `Michael` · `Indiana Jones and the Last Crusade` ·
`Top Gun` · `G.I. Jane` · `Grumpier Old Men`

Item-based collaborative filtering needs nothing but the ratings matrix — no
content features, no user profiles — yet surfaces sensible, taste-aware picks.

## Repository structure

```
.
├── Movie_Recommender.ipynb   # The full pipeline: load → EDA → item-based filtering → my recs
├── u.data                    # MovieLens 100K ratings
├── Movie_Id_Titles           # item_id → title lookup
├── My_Ratings.csv            # My own movie ratings (personal recommendations)
├── requirements.txt          # Python dependencies
├── LICENSE                   # MIT
├── .gitignore
└── README.md
```

## How to run

```bash
# 1. Clone
git clone https://github.com/VinayakMokashi/Movie-Matchmaker.git
cd Movie-Matchmaker

# 2. Install dependencies (a virtual environment is recommended)
python -m venv .venv
# Windows:  .venv\Scripts\activate    |    macOS/Linux:  source .venv/bin/activate
pip install -r requirements.txt

# 3. Launch the notebook and run all cells top to bottom
jupyter notebook Movie_Recommender.ipynb
```

The data files (`u.data`, `Movie_Id_Titles`, `My_Ratings.csv`) are included in
the repo, so the notebook runs end-to-end out of the box. Want your *own*
recommendations? Edit `My_Ratings.csv` with movies you've rated (titles must
match those in `Movie_Id_Titles`) and re-run the final section.

## Future work

- **Hybrid model** — blend item-based and user-based signals for better accuracy.
- **Better similarity** — swap raw Pearson correlation for cosine / adjusted-cosine
  similarity, which handles per-user rating bias more gracefully.
- **Content-based features** — mix in genre, cast and year so brand-new movies
  (with no ratings yet) can still be recommended.
- **Scale** — move to the larger MovieLens datasets (1M / 25M ratings).

## License

Released under the [MIT License](LICENSE). Dataset courtesy of
[GroupLens](https://grouplens.org/datasets/movielens/100k/).

---

*Built by [Vinayak Mokashi](https://github.com/VinayakMokashi).*
