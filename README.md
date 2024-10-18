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

SET color red EX 2 # Set color to red and expire it after 2 secs.

MSET color red car toyota # set multiple key value pairs at the same time.

MGET key1 key2 key2 # get values for multiple keys in a single command.

DEL color # Delete a key and associated value.
```

### 2) Number

```redis
# Very similar command compared to strings - SET, GET, MGET, MSET, DEL; all work with numbers as well.

SET age 20

INCR age # Increment age by 1 --> i.e. age becomes 21
DECR age # Decrment age by 1.

INCRBY age 10 # Increment age by 10
DECRBY age 10 # Decrement age by 10
```
