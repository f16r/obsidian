1. Requirements
	1. Function
		1. Given long URL -> Create Short URL
		2. Given short URL -> Redirect to long URL
	2. Non-Functional
		1. very low latency
		2. very high availability
2. API
	1. POST /create-url
		1. Params: long-url
		2. Status code: 201 Created
	2. GET /{short-url}
		1. Status code: 301 Permanent Redirect
3. Schema
	1. short-url
	2. long-url
	3. created-at
4. How long should the URL be?
	1. 1000 URLs generated per second: 1000 * 60 * 60 * 24 * 365 = 31,5 bn / year
	2. What characters can we use?
		1. 26 (a-z) + 26 (A-Z) + 10 (0 - 9) = 62 characters
	3. 62^7 = 3.5 trillion <- 7 characters
5. Architecture
   ![[Pasted image 20250914231302.png]]
	1. Zookepper gives each instance a range
	2. Instance retrieves range & counts up. Number is used with base62 encoding to generate string
	![[Pasted image 20250914231708.png]]
6. Additional talking points
	1. Analytics
		1. Counts for each URLs to determine which to cache
		2. IP addess to store location information to determine where to locate caches
	2. Rate limiting
		1. Precent DDoS attacks
	3. Security considerations
		1. Add random suffix to the short url to prevent hackers from predicting URLs
	4. Sharding / Partitioning