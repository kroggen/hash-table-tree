# hash-table-tree

This is a data structure that came to my mind when I was thinking about enhancing data access speed on databases.

It implements a hash table on database pages.

It uses 2 types of database pages:

1. Index page
2. Data page

The keys and values are stored on the data pages with a data length before each.

![img1](images/img1.png)

When there is no more free space on a data page to store a new or updated key/value pair we:

1. allocate a new index page
2. choose a new hash nonce
3. reshash all the keys in this page with this new nonce and store the pairs on new pages

![img2](images/img2.png)

So we don't need to rehash the entire database.

## Requirement

The new hash nonce must be different than the previous (in the path up to the root page) so the keys on that new index will be spreaded on separate pages.

## Performance

The performance gain (at least on reads) comes from the amount of pointers on each index page. We can have nearly 1021 pointers in a 4kB page.

A common B-tree with a 4 byte key has half that number of pointers. And with an 8 bytes key the number of pointers is 1/4.

## Limitations

As in any hash table, it only supports unsorted data.

## About the Code

This code is just a proof-of-concept, it does not implement transactions and it is not safe (yet).

## Contact

Bernardo Ramos, Gensis Sistemas

contact 4T litereplica D0T io
