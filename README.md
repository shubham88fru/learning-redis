# learning-redis

# What is Redis?

- Redis is a database (not simply a cache) that is popularly used as a database coz it stores all the data in memory (unlike traditional databases which store it on the disk).
- Redis is really a a database that stores data in the right datastructure (list, set etc.) such that it makes retreival super fast.

## Data types

### 1) Strings - Store and Retreive.

```redis
SET message 'Hi there!'

GET message
```
