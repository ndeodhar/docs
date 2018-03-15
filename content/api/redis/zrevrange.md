---
title: ZREVRANGE
weight: 2392
---

## SYNOPSIS
<b>`ZREVRANGE key start stop [WITHSCORES]`</b><br>
This command returns `members` ordered from highest to lowest score in the specified range at sorted set `key`.
`start` and `stop` represent the high and low index bounds respectively and are zero-indexed. They can also be negative 
numbers indicating offsets from the end of the sorted set, with -1 being the last element of the sorted set, -2 the penultimate element and so on. 
If `key` does not exist, an empty list is returned. If `key` is associated with non sorted-set data, an error is returned.

## RETURN VALUE
Returns a list of members found in the range specified by `start`, `stop`, unless the WITHSCORES option is specified (see below).

## ZREVRANGE Options
<li> WITHSCORES: Makes the command return both the `member` and its `score`.</li>

## EXAMPLES
```{.sh .copy .separator-dollar}
$ ZADD z_key 1.0 v1 2.0 v2 3.0 v3
```
```sh
(integer) 3
```
```{.sh .copy .separator-dollar}
$ ZREVRANGE z_key 0 2
```
```sh
1) "v3"
2) "v2"
3) "v1"
```
```{.sh .copy .separator-dollar}
# With negative indices.
$ ZREVRANGE z_key -2 -1
```
```sh
1) "v2"
2) "v1" 
```
```{.sh .copy .separator-dollar}
# Both positive and negative indices.
$ ZREVRANGE z_key 1 -1 WITHSCORES
```
```sh
1) "v2"
2) "2.0"
3) "v1"
4) "1.0"
```
```{.sh .copy .separator-dollar}
# Exclusive bounds.
$ ZREVRANGE z_key (0 (2
```
```sh
1) "v2"
```

## SEE ALSO
[`zadd`](../zadd/), [`zcard`](../zcard/), [`zrangebyscore`](../zrangebyscore/), [`zrem`](../zrem)