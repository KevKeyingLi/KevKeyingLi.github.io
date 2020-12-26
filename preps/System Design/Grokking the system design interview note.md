# Grokking the system design interview
# 1. System Design Problems
## System Design Interviews: A step by step guide
### Step 1: requirement clarification
Ask system level questions, don't get too much into the details? 

Example
> • Will users of our service be able to post tweets and follow other people?
> • Should we also design to create and display the user’s timeline?
> • Will tweets contain photos and videos?
> • Are we focusing on the backend only or are we developing the front-end too?
> • Will users be able to search tweets?
> • Do we need to display hot trending topics?
> • Will there be any push notification for new (or important) tweets?

### Step 2: System interface definition
Define what APIs are expected from the system.
* establish the exact contract expected from the system
* ensure if we haven’t gotten any requirements wrong

Examples for our Twitter-like service will be:
```
postTweet(user_id, tweet_data, tweet_location, user_location, timestamp, ...)
generateTimeline(user_id, current_time, user_location, ...)
markTweetFavorite(user_id, tweet_id, timestamp, ...)
```

### Step 3: Back-of-the-envelope estimation
estimate the scale of the system. This will also help later on:
* scaling
* partitioning
* load balancing
* caching

> • What scale is expected from the system (e.g., number of new tweets, number of tweet views,
number of timeline generations per sec., etc.)?
> • How much storage will we need? We will have different numbers if users can have photos and videos in their tweets.
> • What network bandwidth usage are we expecting? This will be crucial in deciding how we will manage traffic and balance load between servers.


### Step 4: Defining data model
Defining the data model early will clarify how data will flow among different components of the  system. Later, it will guide towards data partitioning and management.

The candidate should be able to
* identify various entities of the system
* how they will interact with each other
* different aspect of  data management like storage, transportation, encryption, etc. 

Here are some entities for our Twitter like service: 
> User: UserID, Name, Email, DoB, CreationData, LastLogin, etc. 
> Tweet: TweetID, Content, TweetLocation, NumberOfLikes, TimeStamp, etc. 
> UserFollow: UserdID1, UserID2 
> FavoriteTweets: UserID, TweetID, TimeStamp 

Which database system should we use?
* NoSQL vs MySQL-like solution
* What kind of block storage should we use to store photos and videos? 

#### TODO: more reading on block storage, object storage, file storage
* https://cloudacademy.com/blog/object-storage-block-storage/
* https://www.redhat.com/en/topics/data-storage/file-block-object-storage

### Step 5: High-level design 
Draw a block diagram with 5-6 boxes representing the core components of our system. **We should  identify enough components that are needed to solve the actual problem from end-to-end.** 

> For Twitter, at a high-level
> * we will need multiple application servers to serve all the read/write requests
> * with load balancers in front of them for traffic distributions.
> * If we’re assuming that we will have a lot more read traffic (as compared to write), we can decide to have separate servers for handling  these scenarios.
> * On the backend, we need an efficient database that can store all the tweets and can support a huge number of reads.
> * We will also need a distributed file storage system for storing photos and videos.

### Step 6: Detailed design
Dig deeper into two or three components; interviewer’s feedback should always guide us what parts of the system need further discussion. We should be able to **present different approaches, their pros and cons, and explain why we will prefer one approach on the other**. Remember there is no single answer, the **only important thing** is to **consider tradeoffs between different options while keeping system constraints in mind**.
> • Since we will be storing a massive amount of data, how should we partition our data to distribute it to multiple databases? Should we try to store all the data of a user on the same database? What issue could it cause?
> • How will we handle hot users who tweet a lot or follow lots of people?
> • Since users’ timeline will contain the most recent (and relevant) tweets, should we try to store our data in such a way that is optimized for scanning the latest tweets?
> • How much and at which layer should we introduce cache to speed things up?
> • What components need better load balancing?

### Step 7: Identifying and resolving bottlenecks 
Try to discuss as many bottlenecks as possible and different approaches to mitigate them.

> • Is there any single point of failure in our system? What are we doing to mitigate it?
> • Do we have enough replicas of the data so that if we lose a few servers we can still serve our  users?  
> • Similarly, do we have enough copies of different services running such that a few failures will  not cause total system shutdown?  
> • How are we monitoring the performance of our service? Do we get alerts whenever critical  components fail or their performance degrades?  

## Exercise problems
* Designing a URL Shortening service like TinyURL





# 2. Glossary of System Design Basics

# My notes
