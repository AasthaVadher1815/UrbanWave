# UrbanWave
\documentclass{article}
\usepackage{geometry}
\usepackage{listings}
\usepackage{graphicx} % for images
\usepackage{float}    % for [H] option
\usepackage{xcolor}   % for code highlighting
\geometry{margin=1in}

% Setup for code formatting
\lstset{
    basicstyle=\ttfamily\footnotesize,
    breaklines=true,
    frame=single,
    numbers=left,
    numberstyle=\tiny,
    keywordstyle=\color{blue},
    commentstyle=\color{gray},
    stringstyle=\color{red}
}

\title{\textbf{Assignment 4} \\ \vspace{0.5em} UrbanWave: MongoDB Social Media Platform}
\author{\textbf{Aastha Vadher} \\ Roll No: 220228}
\date{}

\begin{document}
\maketitle
\hrule
\vspace{1em}

\section*{Aim}
Design and implement a NoSQL schema for a social media platform called \textbf{UrbanWave} using MongoDB. The platform should support:
\begin{enumerate}
    \item User profiles with India-based locations
    \item Posts and Reels with multiple content categories
    \item Following/Follower relationships
    \item Location-based user discovery
    \item Interest-based recommendations
    \item Content analytics and trending features
\end{enumerate}

\section*{Phase 1: Database Setup \& Data Population}

\subsection*{Sample Data Requirements}

\subsubsection*{Users Sample Data}
\begin{table}[H]
\centering
\begin{tabular}{|l|l|c|l|c|l|}
\hline
\textbf{Username} & \textbf{Full Name} & \textbf{Age} & \textbf{Location} & \textbf{Screen Time (hrs/day)} & \textbf{Interest} \\
\hline
aastha\_01 & Aastha Vadher & 23 & Mumbai & 3.5 & Tech \& Innovation \\
aastha\_02 & Aastha Patel  & 24 & Delhi & 2.8 & Coding \& Startups \\
aastha\_03 & Aastha Sharma & 22 & Bengaluru & 4.1 & Travel \& Food \\
aastha\_04 & Aastha Joshi  & 25 & Pune & 2.5 & Art \& Creativity \\
aastha\_05 & Aastha Mehta  & 23 & Ahmedabad & 3.9 & Coding \& Entrepreneurship \\
aastha\_06 & Aastha Desai  & 24 & Hyderabad & 3.2 & AI \& Machine Learning \\
aastha\_07 & Aastha Raval  & 22 & Jaipur & 2.9 & Nature \& Photography \\
aastha\_08 & Aastha Trivedi & 26 & Surat & 4.4 & Fitness \& Lifestyle \\
aastha\_09 & Aastha Kapoor & 25 & Kolkata & 3.0 & Writing \& Storytelling \\
aastha\_10 & Aastha Bhatt  & 23 & Chandigarh & 3.7 & Motivation \& Self-growth \\
\hline
\end{tabular}
\caption{Users Sample Data}
\end{table}

\subsubsection*{India Cities Coordinates}
\begin{table}[H]
\centering
\begin{tabular}{|l|c|c|}
\hline
\textbf{City} & \textbf{Latitude} & \textbf{Longitude} \\
\hline
Mumbai      & 19.0760 & 72.8777 \\
Delhi       & 28.7041 & 77.1025 \\
Bengaluru   & 12.9716 & 77.5946 \\
Pune        & 18.5204 & 73.8567 \\
Ahmedabad   & 23.0225 & 72.5714 \\
Hyderabad   & 17.3850 & 78.4867 \\
Jaipur      & 26.9124 & 75.7873 \\
Surat       & 21.1702 & 72.8311 \\
Kolkata     & 22.5726 & 88.3639 \\
Chandigarh  & 30.7333 & 76.7794 \\
\hline
\end{tabular}
\caption{India Cities Coordinates}
\end{table}

\section*{Phase 2: Basic Database Operations}

\subsection*{Task 2.1: CRUD Operations}
\begin{enumerate}
    \item Find all users from a specific city:
\begin{lstlisting}[language=JavaScript]
db.users.find(
  { "location.coordinates": [72.8777, 19.0760] }, // Mumbai 
  { _id: 0, username: 1 }
)
\end{lstlisting}
\textbf{Output:}

    \item Find users younger than 25 years:
\begin{lstlisting}[language=JavaScript]
db.users.find(
  { age: { $lt: 25 } }, 
  { _id: 0, username: 1 }
)
\end{lstlisting}
\textbf{Output:}

    \item Find users with screen time greater than 150 minutes:
\begin{lstlisting}[language=JavaScript]
db.users.find(
  { screenTime: { $gt: 2.5 } }, // > 150 minutes
  { _id: 0, username: 1 }
)
\end{lstlisting}
\textbf{Output:}

    \item Update a user’s bio and interests:
\begin{lstlisting}[language=JavaScript]
db.users.updateOne(
  { username: "aastha_01" },
  { $set: { bio: "Tech Enthusiast", interests: ["AI","Cybersecurity","Travel"] } }
)
\end{lstlisting}
\textbf{Output:}

    \item Delete posts older than a specific date:
\begin{lstlisting}[language=JavaScript]
db.posts.deleteMany(
  { createdAt: { $lt: ISODate("2025-08-26T16:45:00.000Z") } }
)
\end{lstlisting}
\textbf{Output:}
\end{enumerate}

\subsection*{Task 2.2: Data Filtering and Sorting}
\begin{enumerate}
    \item Find posts of type \texttt{"reel"} with more than 100 likes:
\begin{lstlisting}[language=JavaScript]
db.posts.find(
  { type: "reel", likes: { $gt: 100 } },
  { _id: 0, caption: 1, content: 1, likes: 1, createdAt: 1 }
)
\end{lstlisting}
\textbf{Output:}

    \item Sort users by followers count (descending):
\begin{lstlisting}[language=JavaScript]
db.users.find(
  {},
  { _id: 0, username: 1 }
).sort({ followersCount: -1 })
\end{lstlisting}
\textbf{Output:}

    \item Find users with specific interests (e.g., \texttt{"travel"} and \texttt{"photography"}):
\begin{lstlisting}[language=JavaScript]
db.users.find({ interests: { $all: ["travel","photography"] } })
\end{lstlisting}
\textbf{Output:}

    \item Get posts from the last 30 days:
\begin{lstlisting}[language=JavaScript]
db.posts.find(
  { createdAt: { $gte: new Date(Date.now() - 30*24*60*60*1000) } },
  { _id: 0, caption: 1 }
)
\end{lstlisting}
\textbf{Output:}

    \item Find inactive users (\texttt{isActive: false}):
\begin{lstlisting}[language=JavaScript]
db.users.find(
  { isActive: false },
  { _id: 0, username: 1, lastSeen: 1 }
)
\end{lstlisting}
\textbf{Output:}
\end{enumerate}

\section*{Phase 3: Geospatial Queries}

\subsection*{Task 3.1: Location-Based Queries}
\begin{enumerate}
    \item Create a \texttt{2dsphere} index on user locations:
\begin{lstlisting}[language=JavaScript]
db.users.createIndex({ location: "2dsphere" })
\end{lstlisting}
\textbf{Output:}

    \item Find users within 1000km radius of Ahmedabad:
\begin{lstlisting}[language=JavaScript]
db.users.aggregate([
  {
    $geoNear: {
      near: { type: "Point", coordinates: [72.5714, 23.0225] },
      distanceField: "distanceInMeters",
      maxDistance: 1000000,
      spherical: true
    }
  },
  {
    $project: {
      _id: 0,
      name: "$username",
      longitude: { $arrayElemAt: ["$location.coordinates", 0] },
      latitude: { $arrayElemAt: ["$location.coordinates", 1] },
      distanceInKm: { $round: [{ $divide: ["$distanceInMeters", 1000] }, 2] }
    }
  }
])
\end{lstlisting}
\textbf{Output:}

    \item Find the nearest user to a given coordinate:
\begin{lstlisting}[language=JavaScript]
db.users.find({
  location: {
    $near: {
      $geometry: { type: "Point", coordinates: [72.6, 23.0] },
      $maxDistance: 1000000
    }
  }
}).limit(1)
\end{lstlisting}
\textbf{Output:}

    \item Get users from multiple cities using the \texttt{$in} operator:
\begin{lstlisting}[language=JavaScript]
db.users.find(
  { "location.city": { $in: ["Mumbai", "Kolkata", "Bengaluru"] } },
  { _id: 0, username: 1, "location.city": 1 }
)
\end{lstlisting}
\textbf{Output:}

    \item Calculate distance between two users (using Haversine formula):
\begin{lstlisting}[language=JavaScript]
db.users.aggregate([
  { $match: { username: { $in: ["Aastha1_123", "Aastha5_567"] } } },
  { $project: { username: 1, city: "$location.city", coordinates: "$location.coordinates" } },
  { $group: { _id: null, users: { $push: "$$ROOT" } } },
  { $project: { user1: { $arrayElemAt: ["$users", 0] }, user2: { $arrayElemAt: ["$users", 1] } } },
  {
    $addFields: {
      distanceInKm: {
        $function: {
          body: function(coords1, coords2) {
            const [lon1, lat1] = coords1;
            const [lon2, lat2] = coords2;
            const toRad = (val) => (val * Math.PI) / 180;
            const R = 6371; // Earth radius in km
            const dLat = toRad(lat2 - lat1);
            const dLon = toRad(lon2 - lon1);
            const a = Math.sin(dLat / 2) ** 2 +
                      Math.cos(toRad(lat1)) * Math.cos(toRad(lat2)) *
                      Math.sin(dLon / 2) ** 2;
            const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
            return R * c;
          },
          args: ["$user1.coordinates", "$user2.coordinates"],
          lang: "js"
        }
      }
    }
  },
  { $project: { _id: 0, "user1.username": 1, "user1.city": 1, "user2.username": 1, "user2.city": 1, distanceInKm: 1 } }
])
\end{lstlisting}
\textbf{Output:}
\end{enumerate}

\section*{Aggregation \& Analytics}

\begin{enumerate}
    \item Trending content (Top 5 most liked posts):
\begin{lstlisting}[language=JavaScript]
db.posts.aggregate([
  { $sort: { likes: -1 } },
  { $limit: 5 }
])
\end{lstlisting}
\textbf{Output:}

    \item Most Active Users (Top 5 by Number of Posts):
\begin{lstlisting}[language=JavaScript]
db.posts.aggregate([
  { $group: { _id: "$userId", totalPosts: { $sum: 1 } } },
  { $sort: { totalPosts: -1 } },
  { $limit: 5 },
  { $lookup: { from: "users", localField: "_id", foreignField: "_id", as: "user" } },
  { $unwind: "$user" },
  { $project: { _id: 0, username: "$user.username", totalPosts: 1 } }
])
\end{lstlisting}
\textbf{Output:}

    \item Top 3 Content Categories (Trending):
\begin{lstlisting}[language=JavaScript]
db.posts.aggregate([
  { $group: { _id: "$category", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 3 }
])
\end{lstlisting}
\textbf{Output:}

    \item User Engagement Score (likes + comments + shares):
\begin{lstlisting}[language=JavaScript]
db.posts.aggregate([
  { $project: { userId: 1, engagement: { $add: ["$likes", "$comments", "$shares"] } } },
  { $group: { _id: "$userId", totalEngagement: { $sum: "$engagement" } } },
  { $sort: { totalEngagement: -1 } },
  { $lookup: { from: "users", localField: "_id", foreignField: "_id", as: "user" } },
  { $unwind: "$user" },
  { $project: { _id: 0, username: "$user.username", totalEngagement: 1 } }
])
\end{lstlisting}
\textbf{Output:}

    \item Top Hashtags Used (Across All Posts):
\begin{lstlisting}[language=JavaScript]
db.posts.aggregate([
  { $unwind: "$hashtags" },
  { $group: { _id: "$hashtags", count: { $sum: 1 } } },
  { $sort: { count: -1 } }
])
\end{lstlisting}
\textbf{Output:}
\end{enumerate}

\section*{Indexing for Performance}

\subsection*{User Collection Indexes}
\begin{lstlisting}[language=JavaScript]
db.users.createIndex({ username: 1 }, { unique: true })
db.users.createIndex({ email: 1 }, { unique: true })
db.users.createIndex({ age: 1 })
db.users.createIndex({ screenTime: -1 })
\end{lstlisting}
\textbf{Output:}

\end{document}
