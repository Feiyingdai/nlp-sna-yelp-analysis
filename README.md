# Yelp Datasets Analysis: Reviews, Users, Businesses & Social Networks

This project presents a comprehensive analysis of the Yelp Open Dataset by integrating multiple perspectives — **textual**, **relational**, and **geospatial**. It combines **Natural Language Processing (NLP)**, **Social Network Analysis (SNA)**, and **Geospatial Visualization** to uncover insights from user reviews, social connections, and physical locations.

## 1. Project Overview

### 1.1 Key Objectives
- Understand **business characteristics**, **user behavior**, and **review sentiment** across cities
- Visualize **spatial distributions** of businesses and **highly active users’ movement patterns**
- Detect **user communities** and **influencers** using network structure
- Identify **key themes and sentiments** in positive and negative reviews

### 1.2 Techniques Used
This project leverages a diverse set of analytical techniques across different domains:

#### Data Wrangling & Exploratory Data Analysis (EDA)
- Merged and filtered multiple datasets (`business`, `review`, `user`) from the Yelp Open Dataset  
- Performed statistical profiling, aggregation, and exploratory visualizations

#### Geospatial Mapping
- Used **Folium** and **Plotly** to visualize:
  - Geographic distribution of businesses  
  - Movement patterns of highly active users across business locations  

#### Natural Language Processing (NLP)
- Conducted sentiment analysis using:
  - **AFINN Lexicon**  
  - **VADER Sentiment Analyzer** (for social media-style text) 
- Extracted:
  - Word frequency and bigrams  
  - Sentiment-specific word clouds  

#### Social Network Analysis (SNA)
- Constructed **user-user friendship graphs** using `networkx`  
- Computed **degree centrality** to identify top influencers  
- Visualized ego networks and overall network topology  

#### Community Detection
- Applied the **Louvain algorithm** to detect tightly-knit user communities  
- Measured **modularity score** to evaluate community structure strength  
- Visualized communities using layout optimization and color-coded nodes  

#### Visualization & Reporting
- Created interactive dashboards using **Tableau** and **Python-based plots**  
- Generated:
  - Network plots  
  - Geospatial heatmaps  
  - Sentiment distribution and trend charts


## 2. Dataset Overview
This project uses the [Yelp Open Dataset](https://www.yelp.com/dataset), which includes six interrelated tables covering businesses, users, reviews, and activity logs. Below is a summary of each dataset and its key columns:

| Dataset               | # Records     | Key Columns                                                           |
|-----------------------|---------------|-----------------------------------------------------------------------------------------------------------------------|
| `yelp_business`       | 174,567       | business_id, name, address, city, state, postal_code, latitude, longitude, stars, review_count, is_open, categories   |
| `yelp_business_hours` | 174,567       | Weekly opening hours for each business (Mon–Sun)                            |
| `yelp_checkin`        | 146,350       | business_id, hour, weekday, checkins                                                                                  |
| `yelp_review`         | 5,261,668     | review_id, user_id, business_id, stars, date, text, useful, funny, cool (feedback from other users)                   |
| `yelp_tip`            | 1,098,324     | text, date, likes, user_id, business_id                          |
| `yelp_user`           | 1,326,100     | user_id, name, review_count, yelping_since, friends, elite (years), fans, Feedback counts (useful, funny, cool)|


## 3. Exploratory Data Analysis (EDA)

### 3.1 Business Overview

#### Star Rating distribution
The majority of Yelp businesses fall within the 3.0 to 4.5 star range, with the highest concentration at 4.0 stars, followed by 3.5 stars and 5.0 stars. This suggests a generally positive sentiment trend among businesses, with relatively few receiving very low ratings.

This distribution aligns with the common observation that users are more likely to leave reviews when they are either highly satisfied or dissatisfied, leading to a polarized rating distribution.

<img width="1025" height="393" alt="Image" src="https://github.com/user-attachments/assets/5425f02f-c2a0-4a41-b278-fd006a0eba74" />


#### Top 20 Categories
Since businesses on Yelp can belong to multiple categories (e.g., "Restaurants; Bars; Nightlife"), we split the categories field by semicolon and retained only the first-listed category to compute the frequency distribution.

As expected, “Restaurants” dominate the platform with 17,842 listings, far exceeding other categories. This is followed by Shopping and Food, confirming Yelp’s primary focus on food and lifestyle services.

These results give a high-level view of what types of businesses are most prevalent on Yelp, and guide deeper segmentation in future analysis (e.g., sentiment by category).

<img width="1280" height="549" alt="Image" src="https://github.com/user-attachments/assets/317c531e-d382-4d65-85f9-e987884850dd" />

#### Geospatial Mapping
To analyze business distribution, we visualized geospatial data at multiple levels by using `latitude` and `longitude` from `yelp_business.csv`:

**Global Level**

A 3D globe map illustrates the worldwide distribution of businesses. The majority are concentrated in North America and parts of Europe.
<img width="486" height="494" alt="Image" src="https://github.com/user-attachments/assets/70bf3a8e-0f6e-40f4-8c29-c942537a5421" />

**District Level**

Heatmaps of North America and Europe show more granular distribution patterns. Dense clusters are visible in U.S. metropolitan areas such as Las Vegas, Phoenix, and Toronto, as well as key European cities like Edinburgh.
<img width="638" height="500" alt="Image" src="https://github.com/user-attachments/assets/23604ba1-14c1-4bca-8f97-332c353a2523" />

<img width="412" height="501" alt="Image" src="https://github.com/user-attachments/assets/2994073f-773a-4abb-83dd-3e30c2da1370" />

**City Level**

The bar chart above displays the top 20 cities with the highest number of businesses in the Yelp dataset.
Given the significantly high business density in Las Vegas, Phoenix, and Toronto, and the presence of Edinburgh among the top 20, we selected these four cities—Las Vegas, Phoenix, Toronto, and Edinburgh—for more detailed city-level geospatial analysis to better understand business clustering and urban patterns.

<img width="1355" height="464" alt="image" src="https://github.com/user-attachments/assets/97f5c351-18a1-4c12-bd8a-ce34aafae74b" />


Detailed scatter plots show the street-level business distribution in selected cities:
- Las Vegas & Phoenix: Businesses are densely packed along main streets and exhibit a clear grid pattern.
- Toronto & Edinburgh: The layouts reflect local geography and urban planning, with Toronto showing linear concentration along main avenues and Edinburgh having a more organic spread.
<img width="1242" height="616" alt="Image" src="https://github.com/user-attachments/assets/fa44c2b8-9847-4a7f-ab39-69e42a155028" />

<img width="1248" height="622" alt="Image" src="https://github.com/user-attachments/assets/d1fbcc14-2051-4d0c-8f4f-e8ce9eef7a4f" />

#### Folium Animation by Star Rating in Las Vegas

()

### 3.2 User Overview
To understand user engagement and the impact of Yelp’s elite user program, we analyze both **active users** and **elite users**:

- **Active users** are defined as users who have posted at least one review, based on the `reviews` table (`user_id` appearing in reviews).
- **Elite users** are identified from the `user` table's `elite` column, where we split multi-year values to determine elite status by year.

#### Active vs Elite Users by Year
- From 2004 to 2017, both active and elite user counts increased significantly.
- Active users grew exponentially, reaching over **450,000** by 2017.
- Elite users increased steadily, but much more selectively — around **35,000** by 2017.
- This highlights that Yelp has scaled its user base while keeping the elite program exclusive.

<img width="1214" height="581" alt="image" src="https://github.com/user-attachments/assets/7eab642a-0370-4b94-871e-19390896d3e9" />

#### Year-over-Year Retention Rate
- **Elite users** consistently show high retention rates (>80%), indicating strong platform loyalty.
- **All users** display a much lower retention rate (~30%), suggesting that most users are casual participants.
- This gap underscores the importance of elite users in sustaining high-quality, ongoing engagement.

<img width="1188" height="580" alt="image" src="https://github.com/user-attachments/assets/f5e514f3-cc84-4c59-a62a-dd9563e6e67a" />


#### Elite vs Non-Elite User Behavior Comparison

- **Elite users** are far more active and socially recognized:
  - They contribute **many more reviews** and attract **significantly more fans**.
  - Their reviews receive higher levels of **useful**, **funny**, and **cool** feedback.
- These stats confirm the **higher quality and influence** of elite contributors on the platform.

| Metric         | Elite Users | Non-Elite Users |
|----------------|-------------|-----------------|
| **Avg Stars**      | 3.85        | 3.70            |
| **Avg Fans**       | 21.94       | 0.47            |
| **Avg Reviews**    | 226.88      | 13.32           |
| **Useful Rate**    | 2.10        | 0.59            |
| **Funny Rate**     | 1.14        | 0.21            |
| **Cool Rate**      | 1.63        | 0.21            |


### 3.3 Review Overview
We randomly sampled 100,000 reviews to explore patterns in user review behavior. The analysis yielded the following key insights:

#### Review Frequency
Most users are infrequent reviewers.
As shown in the left plot, the distribution of reviews per user is highly right-skewed.
Over 80% of users wrote only 1 review, indicating that the majority of Yelp users are one-time contributors.
The cumulative distribution (right plot) confirms this, with nearly all users having submitted fewer than 5 reviews.

<img width="1280" height="594" alt="image" src="https://github.com/user-attachments/assets/90544e43-4eae-426b-895e-04ce80d0452f" />


#### Review Usefulness

We analyzed how the number of "useful" votes a user receives correlates with their behavior:

Higher usefulness correlates with:
Lower ratings (both average and max) — perhaps due to more critical and detailed reviews being perceived as helpful.
Longer review length — reviewers with higher useful counts tend to write more in-depth feedback.
Fewer reviews overall — suggesting that more thoughtful reviewers post less frequently but contribute higher-value content.

<img width="1462" height="375" alt="image" src="https://github.com/user-attachments/assets/a2a8cd74-016b-44cb-a2d4-5d473df6181f" />

#### Review Funny 

We also examined patterns among users who receive more "funny" votes:

Maximum and average ratings tend to decrease as funny votes increase — these reviews may include humorous critiques.
Review length increases — funny reviews also tend to be longer.
Number of reviews decreases — like useful reviews, funny reviews may require more effort and creativity, thus less frequent.

<img width="1472" height="414" alt="image" src="https://github.com/user-attachments/assets/ac60a3aa-b097-4d3f-8b17-17a84caca233" />


### 3.4 Interactive Dashboard
- 使用 Tableau 构建的交互式可视化仪表盘

## 4. Sentiment Analysis
### 4.1 Sentiment by User Groups
- 比较不同用户群体（如精英 vs 非精英）的评论情绪

### 4.2 Word Clouds of Positive and Negative Reviews
- 分析积极与消极评论中的关键词与词云

### 4.3 Key Business Sentiment Deep Dive
- 对重点商户的评论进行情绪趋势追踪和分析（如时间变化、词频变化）

## 5. Social Network Analysis (SNA)
### 5.1 User Friendship Network
- 构建 Yelp 用户好友图，分析节点度、影响者识别

### 5.2 Community Detection with Louvain Algorithm
- Louvain 方法划分社区，输出社区结构、可视化及模块度分析

## 6. Strategic Insights
结合情绪分析与社交网络，提出潜在商业建议，如：
- 精英用户的影响力
- 高情绪分社区
- 商户定位优化
