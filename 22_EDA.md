# Event-Driven Architecture (EDA)
- EDA stands for Event-Driven Architecture. An event is a record of something that has already happened, such as `VideoUploaded`, `OrderPlaced`, or `PaymentCompleted`.

- Before understanding EDA, we need to understand the problem it solves.

- For example, when a user uploads a video to YouTube, multiple services may need to perform tasks such as video transcoding, caption generation, thumbnail creation, and analytics.

- If the video-upload service calls every downstream service synchronously and waits for their responses, it creates runtime dependencies between those services. This can increase latency, limit throughput, complicate scaling, and cause failures to cascade when a downstream service is unavailable.

- EDA addresses this by allowing services to communicate through events.

- For example, the video-upload service publishes a `VideoUploaded` event to a topic. Other interested services subscribe to that topic and process the event independently, without requiring the upload service to call each service directly.

- This reduces direct dependencies between services and enables asynchronous processing. Services can often be scaled independently, and temporary downstream failures can be handled through retries and durable messaging.

- However, these benefits depend on the messaging system and the reliability mechanisms implemented by the application.

- EDA is used to decouple the services and make them more reliable.

- Simple Event Notification : Only limited data is published by producer as event the consumers needs to query the db for more information about event.
- Event-Carried State Transfer : More information about event is send by producer to EDA broker so consumers don't quer the db and make latency more low. 
