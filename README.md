# protoc-gen-go-thanos

My idea is to write a very opinionated protoc Go code generator for the Thanos project. The goals are:

- Allow using `labels.Labels` directly from the Prometheus project to avoid conversion all over the codebase
- Generate function types that are identical to gogo
- Use as few pointers as possible to be GC friendly
- Enable pooling for slices and other things
- Resist adding a ton of options/params/etc. to avoid the same fate as protoc-gen-gogo

In the future, we might also want to add lazy unmarshaling to use in such a setup: Query --> Query --> Store. In this case, the Query in the middle shouldn't have to deserialize everything, only labels. But for this work 100%, we need to somehow differentiate between internal calling of Series() API vs. external.
