## Simulation slow subscriber
<img width="1582" height="961" alt="Screenshot 2026-05-12 at 19 04 15" src="https://github.com/user-attachments/assets/1473e54b-9b12-44d6-8c95-4f91f6a2069b" />

The screenshot displays the slow subscriber simulation, which highlights a clear mismatch between the data production and consumption rates in your event-driven system. The message rates chart shows that the Publish rate peaks quickly as the publisher sends its data at full speed, while the deliver rate is throttled by the artificial delay we have introduced in the subscriber's code. This behavior confirms that the publisher can operate independently of the subscriber's performance, allowing the system to remain responsive even when the final processing stage is significantly slower than the initial data entry.

In this specific screenshot, the total number of queued messages peaks at 1, as shown by the red line in the top chart hitting the 1.0 mark on the Y-axis. This number represents the "backlog" of messages that have successfully reached the AWS broker but are currently waiting for the subscriber to finish its previous task. The count is "as such" because RabbitMQ is performing Load Leveling; it acts as a protective buffer that holds messages in a "Ready" state until the slow subscriber is capable of processing them. This prevents the subscriber from being overwhelmed by a burst of traffic and ensures that no data is lost during the transition from the fast publisher to the throttled consumer.

## Running at least three subscribers

