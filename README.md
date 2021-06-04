# uber
The solution is structured in four different services. For simplicity they are in one project but they can be easily migrated to micro services.  
-	DriverService (managing drivers, with the business logic for adding/removing/activating/deactivating drivers)
-	PassengerService (small service for GUID operations on the passenger table)
-	RidesSerivce (managing rides, from their initial Request status, to contract, to finalizing the ride and creating a past tide entry)
-	RatingSerivce (small service for managing ratings)
-	InitalLoadSerivce (for doing the initial load)

DB is kept simple, with only three tables Drivers, Passengers, and PastRides. In memory H2 is used together with flyway for initial create scripts. Active request, active drivers locations, rating requests are not persisted. 
Initial load makes all entries both drivers and passengers, and activates all drivers. 
All scenarios are covered except of authentication and the pdf print of receipts. Solution is implemented in a way that all endpoints are available even during heavy operations like the initial load (also optimized and fast). For example you can search for active drivers by location while activating drivers.  
UbberAppComplexTest is good walkthrough to the app.  (Didn’t have time to write unit test thought)
Limitation of the current solution because of the small time frame:
-	Its been a while since I have used spring boot, so in order to be able to kick start fast I used an older spring boot project template (which I was using 3 years ago for developing micro services). This is tied to Java 8 (at least the tests), and spring boot . (My InteliJ complains about quite a few things) 
-	Services are not secured, Authentication is omitted, and passwords are not hashed. This is just an additional aspect which is easy to add. 
-	There is no code documentation and no rest service documentation 
-	Logging and exception handling are on the basic level, but with example which shows how this should be done.
-	Strings are used directly, no constants like in productive projects
-	Testing is not complete, just few examples of unit and integration tests
-	Location search performs instantly with all 10K driver entries being active, but this can be further improved with selection algorithm in place of 
