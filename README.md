# Instagram Likes Prediction with Linear Regression

Can we predict how many likes an Instagram post will get? This project builds two linear regression models and shows how one engineered feature improves the predictions.

## Problem

Predict the number of **likes** on an author's latest post using account-level information. The goal was to see how far a simple, interpretable model can go and which feature adds the most value.

## Dataset

- **Source:** `posts.csv`, a dataset of Instagram posts (provided in the Workintech Academy Data Analyst & AI Program)
- **Unit:** one row per post, with author ID (`id`), timestamp (`ts`), `followers`, and `likes`
- **Unique authors:** 9,298
- **Target variable:** `likes`

## Approach

1. **Explored the data:** counted unique authors and plotted followers vs. likes (Plotly), which showed a visible positive relationship
2. **Prepared the data:** sorted posts by date and kept only each author's most recent post, so there is one row per author
3. **Split the data:** 80% train / 20% test
4. **Scaled features** with `StandardScaler`, fitted on the training set only to avoid data leakage
5. **Model 1:** linear regression using `followers` only
6. **Feature engineering:** for each author, calculated `historical_likes`, the **median likes of their previous posts**
7. **Model 2:** linear regression using `followers` + `historical_likes`
8. **Evaluated** both models with R², MSE, and MAE on the test set

## Results

| Model | Features | Test R² | Test MAE |
|---|---|---|---|
| Model 1 | followers | 0.22 | ~33 likes |
| Model 2 | followers + historical likes | **0.56** | **~24 likes** |

![Followers vs Likes](images/followers_vs_likes.png)

## Key Insights

- Follower count alone is a weak predictor: it explains only about 22% of the variation in likes.
- Adding an author's **historical median likes** raised R² from 0.22 to 0.56 and cut the average error from about 33 to about 24 likes.
- Past performance is a much stronger signal than audience size. Two accounts with the same followers can get very different engagement.

## Limitations & Next Steps

- Only two features were used. Post content, posting time, hashtags, and caption length could improve accuracy.
- Likes are skewed (a few posts get very high numbers), so a log transform or a non-linear model might fit better.
- Add `random_state` and cross-validation for more stable, reproducible estimates.
- Check the linear regression assumptions (residual plots, multicollinearity) in more depth.

## Tech Stack

Python • Pandas • Plotly • Scikit-learn • Google Colab

## How to Run

```bash
git clone https://github.com/GuldenizKendigelen/instagram-likes-linear-regression.git
cd instagram-likes-linear-regression
pip install -r requirements.txt
jupyter notebook notebooks/analysis.ipynb
```

## Author

**Guldeniz Kendigelen**: [LinkedIn](https://www.linkedin.com/in/g%C3%BCldeniz-kendigelen-38051b352/) | [GitHub](https://github.com/GuldenizKendigelen)
