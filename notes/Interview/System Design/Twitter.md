
1. Clarification Questions
	1. Q: Can you give me some components to focus on?
		1. A: Timeline, Posting Tweets, User following
	2. Q: Can a tweet contain media like video/photo?
		1. A: Yes, links, photo & video
	3. Q: Timeline (tweets I posted, 4me page with tweets of my followings & ads)
	4. Q: Users can follow each other to subscribe to updates
	5. Q: Do you want me to think about concepts like retweet, search etc.
2. Assumption
	1. Users read more tweets than they publish
	2. When I publish a tweet is it okay to have [[Eventual Consistency]]
		1. When tweet is available in timeline of followers
		2. When tweet is searchable
	3. Most recent data is most important (old tweets do not get accessed very often, while new ones do) but historical data should still be accessible
3. Calculate Metrics (capacity estimation)
	1. Reading
		1. Tweet limited (characters)
			1. UTF-8 is complicated: 1 - 4 bytes per codepoint; on character can be composed of multiple codepoints
			2. one character is 4 bytes; max 200 characters -> 800 bytes -> one tweet 1kb
		2. Users
			1. total users (1B)
			2. active daily users (200M)
			3. avg follower per user (max users also interesting)
		3. Tweets per day (100M) => 2.1 TB / day
			1. 10M Media (200kb x 10M): 2 TB
			2. 90M Text (1kb): 90 GB
		4. Tweets Read per day
			1. 100 per User / day 
			2. 20 bn / day => 20bn / 86400 secs => 232.000 req / sec
		5. Request Size
			1. 20 tweets per request (20kb per request)
			2. Bandwidth: 232000 * 20kb = 4640000kb = 4640mb = 4.64 GB/sec
	2. Writing
		1. Writes per second
4. APIs
	1. POST /v.1.0/tweet
5. Database Design
	1. Tweet
		1. user_id, tweet_id, created_at, type (txt, img), content (either tweet or link to media)
	2. User
		1. user_id, name, email
	3. User Relation
		1. user_id, followed_user_id
6. System components
	1. Post
	2. Follow
	3. Timeline
		1. User timeline
		2. Home timeline