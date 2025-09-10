# 🌊 UrbanWave – MongoDB Social Media Database
## Project Link :-[AasthaVadher_1AUA22BIT134_BDA_Assignment4.pdf](https://github.com/user-attachments/files/22253619/AasthaVadher_1AUA22BIT134_BDA_Assignment4.pdf)

## 🔎 Overview
UrbanWave is a **MongoDB-based project** that models a social media platform.  
It is built to manage **users, posts, and followers**, with support for **location-based features, analytics, and performance optimization**.  

The project demonstrates how NoSQL databases can handle **real-world social media use cases**, including recommendations, trending insights, and influencer tracking.  

---

## ✨ Key Highlights
- 👤 **User Profiles** with personal details, interests, and activity.  
- 🖼️ **Posts & Reels** with captions, hashtags, likes, shares, and views.  
- 🔗 **Follower System** to manage connections.  
- 🌍 **Geospatial Features** for nearby user discovery.  
- 📈 **Analytics with Aggregation** to track trends and engagement.  
- ⚡ **Performance Indexing** for scalable queries.  
- 📱 **Real-world Social Features** like influencer ranking and personalized feeds.  

---

## 🗂️ Data Model

### 👥 Users
Stores key user information:  
- Username, full name, email (unique)  
- Age, bio, interests  
- Location in **GeoJSON** format  
- Screen time, follower/following counts  
- Status and activity timestamps  

### 🖼️ Posts
Represents user-generated content:  
- Linked to a specific `userId`  
- Type: **post** or **reel**  
- Content category, caption, hashtags  
- Location (GeoJSON Point)  
- Metrics: likes, comments, shares, views  
- Creation date  

### 🔗 Followers
Manages social connections:  
- `followerId` and `followingId`  
- Relationship creation timestamp  

---

## ⚙️ Implementation Phases

### 📌 Phase 1 – Setup & Data Population
- Created **UrbanWave** database  
- Collections: `users`, `posts`, `followers`  
- Schema validation applied  
- Inserted sample users, posts, and follower data  

### 📌 Phase 2 – CRUD & Filtering
- Manage user details  
- Find and filter based on age, city, screen time  
- Update user bios and interests  
- Remove old posts  
- Sort users by popularity  

### 📌 Phase 3 – Geospatial Queries
- Enabled **2dsphere indexing**  
- Find nearest users  
- Get users from multiple cities  
- Calculate distances between users  

### 📌 Phase 4 – Analytics & Insights
- Top 5 most liked posts  
- Most active users  
- Trending content categories  
- User engagement scores  
- Popular hashtags  

---

## 💡 Special Features
- 📍 **Location-aware recommendations**  
- 🔥 **Trending insights** for content & hashtags  
- ⭐ **Influencer ranking** based on followers & engagement  
- 🚀 **Performance optimization** with smart indexing  
- 📊 **Actionable analytics** for real-world scenarios  

---

## 📷 Screenshots
 Schema


 Users Data schema  <img width="1431" height="783" alt="Screenshot 2025-09-10 at 4 38 08 PM" src="https://github.com/user-attachments/assets/6f079cc4-ec91-4429-9f13-4ed9abb80b95" /> 
Posts schema <img width="1431" height="783" alt="Screenshot 2025-09-10 at 4 40 49 PM" src="https://github.com/user-attachments/assets/15644f9e-29ac-4062-b63c-66b905d6bd63" />
 Followers data Schema Dashboard <img width="1431" height="783" alt="Screenshot 2025-09-10 at 4 42 13 PM" src="https://github.com/user-attachments/assets/ed66ce85-a617-4131-a4f6-031e2b482b6c" />



## 🚀 Running the Project
1. Install [MongoDB Community Edition](https://www.mongodb.com/try/download/community).  
2. Clone this repository:  
   ```bash
   git clone https://github.com/your-username/urbanwave.git
   cd urbanwave
