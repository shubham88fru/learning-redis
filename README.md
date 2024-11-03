# learning-redis

# What is Redis?

- Redis is a database (not just a cache) that is popularly used as a database coz it stores all the data in memory (unlike traditional databases which store it on the disk).
- Redis is really a database that stores data in the right datastructure (list, set etc.) such that it makes retreival super fast.

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

### 3) Hash

```redis
# Purpose is to store a hastable of sorts against a key.
# Important to note that redis doesn't allow nested hash (Map<Map<..>>) to be stored as value.

HSET company name 'Some Co.' since 1915 # equivalent to storing -> ["company": { "name": "Some Co.", "since": "1915" }]

HGET company name # Get the field `name` from the map stored at key `company`

HGETALL company # Get the entire map stored at key `company` --> { "name": "Some Co.", "since": "1915" }

HEXISTS company age # Check if a field `age` exists in the map stored at key `company`.

DEL company # Delete the entire hash stored at key `company`. (Note: No `H` in this command)

HDEL company age # Delete a (`age` in this case) field from the hash stored at the key.

HINCRBY company age 10 # Increment the value of field `age` by 10 in the hash stored at key `company`.

HSTRLEN company name # Get length of the value stored at field `name` in the hash stored at `company`.

HKEYS company # Get all the keys from the hash stored at `company`.

HVALUES company # Get all the values from the hash stored at `company`.

```

### 4) Set

```redis

SADD colors red blue # Add values `red` and `blue` to set called `colors`

SMEMEBERS colors # Get all entries of set `colors`

SUNION colors:1 colors:2 colors:3 # Get union of values in sets `colors:1`, `colors:2`, and `colors:3`

SINTER colors:1 colors:2 colors:3 # Get the intersection of the values in sets `colors:1`, `colors:2`, and `colors:3`

DIFF colors:1 colors:2 colors:3 # Return elements that exist in the first set, but not any others

SINTERSTORE colors:results colors:1 colors:2 colors:3 # Do an intersection of `colors:1`, `colors:2`, and `colors:3` and store results in set `colros:results`

SISIMEMEBER colors:1 red # Return true or false depending on whether the value `red` is or isn't present in the set

SCARD colors:1 # Return the number of elements in set `colors:1`

SREM colors:1 red # Remove value red from set `colors:1`

SSCAN colors:1 0 COUNT 2 # Scan through all the elements in a set. In this case, get 2 elements on page 0.
```

#### 4.1) Sorted Sets

```redis
# A mix of a hash and a set. No `keys` and `values`. There are `members`
# and `scores`.

# `Members` are unique. `Scores` don't have to be unique.
# `Scores` are sorted from least to greatest.

ZADD products 45 monitor # Adds a member-score pair to a sorted set. In this case, add `score` 45 to a `member` monitor in the sorted set `products`.

ZSCORE products monitor # Get the score of a member. In this case, score of monitor member from the products sorted set.

ZREM products monitor # Remove a member from a sorted set. In this case, remove the member monitor from the sorted set products.

ZCARD prodcuts # Get the number of members in sorted set products.

ZCOUNT products 0 50 # Get the number of members in a sorted set within a range of scores. In this case, memebers with score >= 0 && scores <= 50 from products sorted set.

ZPOPMIN products 2 # Remove and return some number of the lowest score pairs. In this case, remove the 2 entries with lowest scores and return them.

ZPOPMAX products 2 # Remove and return some number of the highest score pairs. In this case, remove the 2 entries with highest scores and return them.

ZINCRBY products 15 keyboard # Adjust a member's score by the given amount. In this case, increment `keyboard`'s score by 15 in the `products` sorted set.

ZRANGE products 15 1 2 # Retrieve a range of members and (optionally) scores (by Adding WITHSCORES at the end). In this case, get all members (not the scores) in range (index) 1 to 2.

# Sort command operates on `members` not the `score`.
# Confusingly, the Sort command refers to these members as
# 'scores' (not members).
# SORT command works on Sets, Sorted Sets and Lists only.

SORT books:likes ALPHA # Sort the sorted set `books:likes` by the members lexicographically.
SORT books:likes BY books:*->year # Sort by.
SORT books:likes BY books:*->year GET books:*->title GET books:*->year
SORT books:likes BY nosort GET # GET books:*->title GET books:*->year # No sorting. Just Join.
```

### 5) HyperLogLog

```redis
# HyperLogLog is an algorithm for approximately counting the number
# of unique elements.
# It's similar to set, but doesn't actually store the elements. It somehow
# through the use of math and complicated algorithms, just 'remembers' whether or not
# a value was previously added in it.

PFADD vegetables celery # Add a value `celery` in the hyperloglog named `vegetables`.
PFCOUNT vegetables # returns the 'approximate' count of values in the hyperloglog `vegetables`.

```
