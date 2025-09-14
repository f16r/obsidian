1. Catalog the details your interviewer has given you
2. Requirements (==**find out the key details**==)
	1. Functional
		1. What features do we need?
		2. Who are our users?
		3. What's the expected usage pattern?
	2. Non-Functional
		1. Latency requirements?
		2. Read-to-write-ratio?
		3. Metrics
			1. Reads per second
			2. Write per second
			3. Required storage
3. API Design?
4. DB Schema?
5. System Components
	1. Start with big picture first before going into details
	2. No over-engineering
		1. Explain easy solution and then go into steps which might be necessary for scaling (load balancer -> multiple instances -> caches -> partitioning -> sharding) 