# Steps
1. Catalog the details your interviewer has given you
	1. Repeat / Write down what you have understood
	2. Ask if everything is mentioned
2. Requirements (==**find out the key details**==)
	1. Functional
		1. What features do we need?
		2. Who are our users?
		3. What's the expected usage pattern?
	2. Non-Functional
		1. Latency requirements?
		2. Read-to-write-ratio?
		3. Geography of the users
		4. Geo-political constraints
		5. Platform (Mobile / Desktop)
		6. Metrics
			1. Reads per second
			2. Write per second
			3. Required storage
			4. Active users!
3. API Design?
4. DB Schema?
5. System Components
	1. Start with big picture first before going into details
	2. No over-engineering
		1. Explain easy solution and then go into steps which might be necessary for scaling (load balancer -> multiple instances -> caches -> partitioning -> sharding) 
# Principles
1. Communicate efficiently
	1. Explain what you are thinking
2. Scope the problem
	1. Before starting Ask Questions / Tease out the information
	2. Do not start unprepared!!
3. Drawing (too soon -> you might not understand the problem)
4. Start with a simple design (but mention optimizations)
5. Properly understand the problem
6. Practice
	1. Reduce stress level
7. Explain you thinking
	1. Which database
		1. SQL: Join, Multiple Tables
		2. NoSQL:
		3. BLOP Storage
8. Get comfortable with the math
	1. Assumptions 
		1. One Instance can handle roughly 1000 req/sec
		2. 1bn Queries a day -> traffic for queries 
			1. e.g. avg. 1000/sec
			2. peak 2000/sec
	2. Load balancing based on signals
		1. Bandwidth
		2. CPU utilization
		3. Memory consumption
	3. Units 
		1. kb/mb/gb/tb/pb
		2. Storage bytes / network bits (8 bits -> 1 byte)
9. Drawing
	1. Box, text, arrow