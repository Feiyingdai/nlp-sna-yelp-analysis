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

### Data Wrangling & Exploratory Data Analysis (EDA)
- Merged and filtered multiple datasets (`business`, `review`, `user`) from the Yelp Open Dataset  
- Performed statistical profiling, aggregation, and exploratory visualizations

### Geospatial Mapping
- Used **Folium** and **Plotly** to visualize:
  - Geographic distribution of businesses  
  - Movement patterns of highly active users across business locations  

### Natural Language Processing (NLP)
- Conducted sentiment analysis using:
  - **AFINN Lexicon**  
  - **VADER Sentiment Analyzer** (for social media-style text) 
- Extracted:
  - Word frequency and bigrams  
  - Sentiment-specific word clouds  

### Social Network Analysis (SNA)
- Constructed **user-user friendship graphs** using `networkx`  
- Computed **degree centrality** to identify top influencers  
- Visualized ego networks and overall network topology  

### Community Detection
- Applied the **Louvain algorithm** to detect tightly-knit user communities  
- Measured **modularity score** to evaluate community structure strength  
- Visualized communities using layout optimization and color-coded nodes  

### Visualization & Reporting
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
- 商户类型、位置分布、评分等基础统计分析

### 3.2 User Overview
- 用户活跃度、精英用户分析、用户评分行为

### 3.3 Review Overview
- 评论数量、情感分布、时间趋势

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
