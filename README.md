# learning-redis

# What is Redis?

- Redis is a database (not just a cache) that is popularly used as a database coz it stores all the data in memory (unlike traditional databases which store it on the disk).
- Redis is really a a database that stores data in the right datastructure (list, set etc.) such that it makes retreival super fast.

## Data types

### 1) Strings - Store and Retreive.

```redis
SET message 'Hi there!' # Set a key message with value 'Hi There!'

GET message # Get the value of a key named message.

SET message green GET # Set the key message to green and Get previous value

SET existingKey 'value' XX # Set existingKey to 'value' if and only if the key exists already.

SET newKey 'value' NX # Set newKey to 'value' if and only if the key doesn't exist already.
```
