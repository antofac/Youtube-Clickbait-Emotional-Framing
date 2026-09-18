# Clickbait and Emotional Framing: An Analysis of YouTube News Channels

## Research Question
How do alternative and mainstream news channels differ in their use of clickbait and emotional language on YouTube, and how does this relate to audience engagement and interaction?

**Hypothesis:** alternative channels rely on stronger negative emotional framing (fear, anger), generating higher but more volatile engagement, while mainstream channels show more stable reactions through neutral framing.

## Data
- **Source:** YouTube Data API v3, collected via a dedicated data collection and preprocessing pipeline.
- **Channels:** BBC News and CNN (mainstream), The Young Turks and The Jimmy Dore Show (alternative).
- **Main dataset:** 2,608 videos and 451,047 comments, October 2025 – January 2026 (video metadata: title, description, publish date, engagement metrics; comment data: text, author, likes, timestamps).
- **Network dataset:** due to API limits, restricted to the most recent 15 days (Jan 5–20, 2026): the top 1,500 most-liked comments per channel, with up to 20 replies fetched per comment (10,456 replies total).

## Methodology
A mixed-methods pipeline combining descriptive statistics, NLP, and network analysis, entirely in Python:

1. **Exploratory analysis:** temporal patterns of video production and comment activity; engagement distributions per channel.
2. **Clickbait operationalization:** built from scratch using lexical (trigger words, superlatives), structural (punctuation intensity, uppercase ratio, title length), and behavioral indicators, rather than relying on an off-the-shelf classifier.
3. **Text preprocessing:** lowercasing, URL/punctuation removal, stopword filtering, lemmatization (SpaCy), emoji and short-token removal — applied separately to titles/descriptions and to comments due to dataset size.
4. **Linguistic analysis:** topic modeling with LDA (Gensim, 5 topics per channel, run separately on titles alone and on titles+descriptions), sentiment analysis (VADER), and discrete emotion detection across 8 emotions (NRCLex).
5. **Network analysis:** directed reply networks (NetworkX) built per channel, with degree, density, and connected components as key metrics; visualization restricted to nodes with degree ≥ 5.

## Results
- **Clickbait ≠ engagement:** alternative channels use more lexical and structural clickbait markers, but these only weakly correlate with comment volume — engagement is driven more by thematic salience (polarizing topics like elections, war, scandal) than by headline formatting.
- **Framing differs by channel type:** mainstream channels use institutional, event-driven language with a neutral lexical style; alternative channels favor personalized, host-centered narratives designed to evoke moral outrage.
- **A production–reaction split in alternative channels:** their titles skew toward fear and anger, but their descriptions skew toward trust and joy — a branding/retention strategy not present in mainstream channels, where titles and descriptions stay emotionally consistent.
- **Weaker title-to-comment sentiment correlation in alternative channels** (r ≈ 0.30 vs. r ≈ 0.37–0.42 for mainstream), suggesting their audiences respond more to pre-existing ideological alignment than to any single video's framing — consistent with echo-chamber dynamics.
- **Network structure differs by channel type:** BBC News shows a broad, broadcast-style network with several high-degree hubs; alternative channels show denser, more centralized peer-to-peer interaction.
- Based on these patterns, channels were re-grouped into three types rather than a simple mainstream/alternative split: an institutional broadcaster (BBC), commercial/partisan leaders relying on volatile, event-driven spikes (CNN, TYT), and a niche radical channel with intense but limited participation (TJDS).

## Limitations
- Reported correlations are descriptive and were not tested for statistical significance or corrected for multiple comparisons; with hundreds of thousands of observations, even weak correlations can appear "significant" without being practically meaningful.
- The number of LDA topics (5) was fixed for interpretability rather than selected via a coherence-score search.
- CNN's smaller, sparser network partly reflects a drop in its video publishing frequency during the sampling window, not necessarily lower audience engagement — a sampling limitation rather than a substantive finding.

## Tools
Python, pandas, spaCy, NLTK, Gensim (LDA), VADER, NRCLex, NetworkX, YouTube Data API v3.
