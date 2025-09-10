# **UrbanWave MongoDB Project**

## **Introduction**
UrbanWave is a MongoDB-based **social media platform** designed to manage **users**, **posts**, and **followers**.  
The project implements location-based discovery, analytics, and real-world social media features such as trending posts, engagement scores, and influencer tracking.  

---

## **Project Features**
- 👥 **User Profiles** → with personal details, activity status, and location.  
- 🎬 **Posts & Reels** → likes, comments, shares, views, captions, and hashtags.  
- 🔗 **Followers & Following** → relationship management.  
- 📍 **Geospatial Queries** → find nearest users, within radius, and across cities.  
- 📊 **Analytics & Insights** → engagement, trending categories, top hashtags.  
- ⚡ **Indexes** → improve performance on frequent queries.  
- 📱 **Real-World Functionalities** → personalized feeds, trending sections, influencer discovery.  

---

## **Design Decisions**

### 1. Collections
- **Users** → stores account details, location (GeoJSON), screen time, and activity.  
- **Posts** → stores posts/reels with metadata (likes, hashtags, createdAt).  
- **Followers** → manages who follows whom.  

### 2. Relationships with ObjectId
- `userId` in **Posts** → links to `_id` in **Users**.  
- `followerId` & `followingId` in **Followers** → link to **Users**.  
- Ensures data remains consistent and connected.  

### 3. Location Data
- Stored in **GeoJSON** format.  
- Enables queries like: *find users within 100km of Ahmedabad*.  

### 4. Indexes for Speed
- `2dsphere` index on **location** → for geospatial lookups.  
- Indexes on `createdAt`, `followersCount`, `screenTime`, `username`.  
- Boosts query performance in large datasets.  

### 5. Aggregation for Analytics
- Top 5 trending posts (by likes).  
- Most active users (by number of posts).  
- Top content categories.  
- User engagement score (likes + comments + shares).  
- Trending hashtags.  

### 6. Scalability
- Used **references** instead of embedding for flexibility.  
- Prevents data duplication and supports future expansion.  

### 7. Real-World Features
- Trending hashtags & content.  
- Influencer detection based on followers & engagement.  
- Personalized recommendations using user interests & location.  

---

## **Sample Queries**
- Find all users from Mumbai.  
- Get posts with more than 100 likes.  
- Find users younger than 25.  
- Get nearby users within 100km radius.  
- Calculate distance between two users.  

---

## **Project Documentation**
📄 Full report: [UrbanWave.pdf](https://github.com/user-attachments/files/22253163/UrbanWave.pdf)


