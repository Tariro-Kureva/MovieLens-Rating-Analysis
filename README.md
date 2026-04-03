 # 🎬 What Makes a Movie Worth Watching?
### A deep dive into 26M user ratings — genre appeal, user behavior & the anatomy of a great film

> *Spoiler: Popularity is a lie. Shawshank Redemption proves it.*

**Author:** Tariro Kureva

---

## 🎯 The Big Question
Streaming platforms recommend what's *popular* — but popular doesn't mean *good*. This project digs into 26 million real user ratings to find out what actually separates a 4.5★ film from a 2.0★ one — and builds a recommendation engine that prioritizes quality over hype.

---

## 💥 The Numbers That Tell the Story

| Stat | Value |
|------|-------|
| 🎬 Total ratings analyzed | 26 million |
| 🎥 Movies covered | ~45,000 |
| 👥 Unique users | 270,000 |
| ⭐ Global average rating | 3.53★ |
| 🏆 Highest rated film | Shawshank Redemption (4.43★) |
| 🔥 Most common rating | 4.0★ (28.1% of all ratings) |
| 🤝 Max item-item similarity | 0.87 (Shawshank ↔ Green Mile) |

---

## 🔑 Key Findings

### 1. Niche beats mainstream — every time
Film-Noir (4.01★), War (3.79★) and Documentary (3.73★) outscore blockbuster genres like Action (3.41★) and Comedy (3.42★). Critical depth drives quality, not audience size.

### 2. Popularity ≠ Quality
Forrest Gump has 341K ratings but scores 4.01★. Shawshank has 30K fewer ratings but scores 4.43★. The most-watched film is rarely the best-rated one.

### 3. Audiences skew positive
60%+ of all ratings are 3.5★ or higher. 4.0★ is the single most common rating. Self-selection bias is real — MovieLens users are enthusiasts, not casual viewers.

### 4. Classic cinema ages like fine wine
Pre-2000 films accumulate higher scores over time as cinephiles selectively rate them. Rating activity peaked around 2002 then stabilised.

### 5. 8 emotional words predict a review's sentiment better than anything else
(See companion IMDB Sentiment Analysis project)

---

## 🎥 Top 5 Films by Quality Score
| Rank | Title | Ratings | Score |
|------|-------|---------|-------|
| 🥇 | Shawshank Redemption (1994) | 311K | 4.43★ |
| 🥈 | The Godfather (1972) | 265K | 4.36★ |
| 🥉 | Schindler's List (1993) | 325K | 4.25★ |
| 4 | Pulp Fiction (1994) | 307K | 4.20★ |
| 5 | Fargo (1996) | 278K | 4.10★ |

---

## 🤖 Collaborative Filtering Engine

Built two recommendation models from scratch using cosine similarity:

### User-User CF
> *"Find me users who watch what I watch — then show me what they loved that I haven't seen yet"*
- Pivot → User×Movie matrix
- Cosine-normalize rows
- Top-10 similar users → rank unseen movies by weighted average rating

### Item-Item CF
> *"If you loved Shawshank, here's what comes next..."*
- Transpose to Movie×User matrix
- Cosine similarity → Top-15 similar films

**Sample output — Similar to Shawshank Redemption (1994):**
| Film | Similarity |
|------|-----------|
| The Green Mile (1999) | 0.87 |
| Schindler's List (1993) | 0.81 |
| The Godfather (1972) | 0.79 |
| Forrest Gump (1994) | 0.74 |
| 12 Angry Men (1957) | 0.71 |

---

## 🛠️ Methods & Pipeline

```
26M ratings
    ↓
Sample 10K rows (random_state=42)
    ↓
pivot_table() → User×Movie matrix (NaN=0)
    ↓
normalize(axis=1) → cosine-normalize rows
    ↓
cosine_similarity() → N×N similarity matrix
    ↓
sort + filter → exclude seen items
    ↓
Top-10 similar users / Top-15 similar films
```

**Analysis methods used:**
- Descriptive Statistics — mean, median, distribution of 0.5–5.0 scale
- Correlation Analysis — rating count vs average score
- Genre Segmentation — average ratings and volume per genre
- Temporal Trend Analysis — rating activity by year
- Collaborative Filtering — cosine similarity, user-user and item-item

---

## 📦 Dataset
- **Source:** MovieLens (Kaggle/GroupLens)
- **Size:** 26M ratings, ~45,000 movies, 270,000 users, through July 2017
- **Files:** `ratings.csv` (userId, movieId, rating, timestamp) + `movies.csv`
- **Rating scale:** 0.5–5.0 in half-star steps

---

## 💡 Business Recommendations

**1. Surface niche high-rating genres prominently**
Promote Film-Noir, War and Documentary — high quality but buried by volume-heavy genres

**2. Separate popularity from quality in rankings**
Display "Critically Loved" vs "Most Watched" — Shawshank (4.43★) outperforms everything

**3. Weight ratings by user engagement history**
Positive skew from casual users — down-weight first-time raters for accuracy

**4. Re-engage audiences with classic cinema**
Pre-2000 films earn high cinephile ratings — curated campaigns can reactivate dormant users

---

## ⚠️ Limitations
- Data covers ratings through July 2017 — post-streaming-wars era not reflected
- No demographic data — audience segment analysis not possible
- Self-selection bias: MovieLens users are enthusiasts, scores may be inflated
- Cold-start problem: no history for new users or movies (fix: hybrid CF + content-based filtering)

---

## 🔧 Tools & Libraries
- Python
- Pandas / NumPy
- Scikit-learn (cosine_similarity, normalize)
- Matplotlib / Seaborn
- Collaborative Filtering (custom pipeline)

---

## 📁 Files
| File | Description |
|------|-------------|
| `movie_poster_final.pdf` | Full research poster with all findings and visualizations |

---

## 🔗 Related Project
👉 [IMDB Sentiment Analysis — What Makes Movie Reviews Positive?](https://github.com/Tariro-Kureva/IMDB-Sentiment-Analysis-NLP)

---

*Last updated: April 2026*

