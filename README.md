# News Coverage on YouTube: Topics, Tone and Audience Interaction

A text and network analysis comparing how two international broadcasters, BBC News and Al Jazeera English, covered events in the Middle East on YouTube between October 2024 and January 2025, and how their audiences responded in the comments.

Course project, M.Sc. Data Analytics for Business and Society, Ca' Foscari University of Venice (January 2025).

This is a methods project. It describes language and interaction patterns in the data and takes no position on the events covered.

## Questions

1. Which topics dominate each channel's video titles, descriptions and comment sections?
2. How does the tone of the coverage compare with the tone of audience comments?
3. How do commenters interact with each other on each channel?

## Data

Collected with the YouTube Data API v3 from one playlist per channel.

| | BBC News | Al Jazeera English |
|---|---|---|
| Videos | 49 | 50 |
| Top-level comments | 5,826 | 4,295 |
| Replies | 1,583 | 183 |

Videos were published between 9 October 2024 and 17 January 2025. The raw comment data is not stored in this repository because it contains commenters' names and texts; `01_data_collection.ipynb` reproduces the collection with your own API key.

## Methods

- **Topic modelling:** Latent Dirichlet Allocation on bag-of-words counts (scikit-learn), run separately on titles, descriptions and comments for each channel, with a 2-D PCA view of the topics.
- **Sentiment:** TextBlob polarity for titles, descriptions and comments; VADER intensity categories for comments.
- **Emotion classification:** a pretrained DistilRoBERTa emotion model (`j-hartmann/emotion-english-distilroberta-base`) applied to unique comments.
- **Network analysis:** directed reply networks between commenters (NetworkX), with degree and betweenness centrality and community detection.

## Findings

- **Audience interaction differs sharply.** BBC comment sections contain 1,583 replies against 183 on Al Jazeera. The BBC reply network has 1,121 users, 1,261 links and 157 communities; the Al Jazeera network has 145 users, 141 links and 25 communities.
- **Emotion profiles are similar.** After "neutral", anger is the most frequent emotion on both channels (22% of unique BBC comments, 21% of unique Al Jazeera comments), followed by disgust (14% and 10%). Joy is the least frequent emotion under BBC videos (4%) and more common under Al Jazeera videos (8%).

Topic tables and sentiment distributions for titles, descriptions and comments are in `02_analysis.ipynb`.

## Limitations

- Two playlists and about one hundred videos are a small, non-random sample of each channel's output.
- Lexicon-based sentiment tools (TextBlob, VADER) were built for reviews and social media posts and are unreliable on news about conflict, where negative words are descriptive.
- The emotion model was trained on other English text and was not validated on this data.
- Only English-language text is analysed, and commenters are not representative of any wider population.

## Tools

Python, google-api-python-client, pandas, scikit-learn, NLTK, TextBlob, VADER, Hugging Face Transformers, NetworkX, Matplotlib, Seaborn, WordCloud.

## Repository

```
├── 01_data_collection.ipynb   # YouTube Data API collection and preprocessing
├── 02_analysis.ipynb          # topics, sentiment, emotions, networks
├── requirements.txt
└── README.md
```
