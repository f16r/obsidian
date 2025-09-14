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