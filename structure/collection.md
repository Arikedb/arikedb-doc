## Arikedb Collection
In Arikedb, [variables](/structure/variable.md) are grouped into collections. A collections is just a set of variables which can be accessed in the same index. All commands to read and write values can be performed over a set of multiple variables in a single call, making the process much more faster, but they must be performed over one collection at a time, since the variables index is one per collection.

An Arikedb collection has next metadata:
 - **name**: This property defines the name of the collection. It is a unique and human readable identifier in each arikedb server or cluster deploy. Any operation made over variables needs to refer a collection by its name.
