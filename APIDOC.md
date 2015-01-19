# API Documentation

## Constructors

The following constructor functions can be used to create different kind of streams.

##### Stream(collection)

Returns a new stream for the given collection. Collection can either be an array or an object hash (map).

##### Stream(string)

Returns a new stream for the given string. The string will be splitted by characters.

##### Stream.of(args...)

Returns a new stream for the given arguments.

##### Stream.empty

Returns a new empty stream.

##### Stream.range(startInclusive, endExclusive)

Returns a new stream for the given number range.

##### Stream.rangeClosed(startInclusive, endInclusive)

Returns a new stream for the given number range.

##### Stream.generate(supplier)

Returns a new infinite stream. The elements of the stream are generated by the given supplier function.

##### Stream.iterate(seed, fn)

Returns a new infinite stream. The elements of the stream are generated by utilizing the given iterator function, starting with `seed` at n=0, then calling fn(seed) for n=1, fn(fn(seed)) for n=2 etc.

## Intermediate Operations

Intermediate operations all return a stream, thus enabling you to chain multiple operations one after another without using semicolons.

##### filter(predicate)

Filters the elements of the stream to match the given predicate function and returns the stream.

##### filter(regexp)

Filters the elements of the stream to match the given regular expression and returns the stream.

##### map(mappingFn)

Applies the given mapping function to each element of the stream and returns the stream.

##### map(path)

Maps each element of the stream by resolving the given string `path` and returns the stream.

E.g. `map('a.b.c')` is equivalent to `map(function(obj) { return obj.a.b.c; })`.

##### flatMap(mappingFn)

Applies the given mapping function to each element of the stream and flattens the results by replacing each element with the contents of the element in case of collections, then returns the stream.

##### flatMap(path)

Maps each element of the stream by resolving the given string `path` and flattens the results by replacing each elemet with the contents of the element in case of collections, then returns the stream.

E.g. `flatMap('a.b.c')` is equivalent to `flatMap(function(obj) { return obj.a.b.c; })`.

##### sorted()

Sorts the elements of the stream according to the natural order and returns the stream.

Alias: `sort`

##### sorted(comparator)

Sorts the elements of the stream according to the given comparator and returns the stream.

Alias: `sort`

##### distinct()

Returns the stream consisting of the distinct elements of this stream.

##### limit(maxSize)

Truncates the elements of the stream to be no longer than `maxSize` and returns the stream.

##### skip(n)

Discards the first `n` elements and returns the stream.

##### peek(consumer)

Performs the consumer function for each element and returns the stream.

## Terminal Operations

Terminal operations return a result (or nothing), so each streaming pipeline consists of 0 to n intermediate operations followed by exactly one terminal operation.

##### toArray()

Returns an array containing the elements of the stream.

Alias: `toList`

##### forEach(consumer)

Performs the consumer function for each element of the stream.

Alias: `each`

##### findFirst()

Returns an `Optional` wrapping the first element of the stream or `Optional.empty()` if the stream is empty.

Alias: `findAny`

##### min()

Returns an `Optional` wrapping the minimum element of the stream (according the natural order) or `Optional.empty()` if the stream is empty.

##### min(comparator)

Returns an `Optional` wrapping the minimum element of the stream (according the given comparator function) or `Optional.empty()` if the stream is empty.

##### max()

Returns an `Optional` wrapping the maximum element of the stream (according the natural order) or `Optional.empty()` if the stream is empty.

##### max(comparator)

Returns an `Optional` wrapping the maximum element of the stream (according the given comparator function) or `Optional.empty()` if the stream is empty.

##### sum()

Returns the sum of all elements in this stream.

##### average()

Returns an `Optional` wrapping the arithmetic mean of all elements of this stream or `Optional.empty()` if the stream is empty.

Alias: `avg`

##### count()

Returns the number of elements of the stream.

Alias: `size`

##### allMatch(predicate)

Returns whether all elements of the stream match the given predicate function.

##### anyMatch(predicate)

Returns whether any element of the stream matches the given predicate function.

##### noneMatch(predicate)

Returns whether no element of the stream matches the given predicate function.

##### collect(collector)

Performs a generalized reduction operation denoted by the given collector and returns the reduced value. A collector consists of a supplier function, an accumulator function and an optional finisher function.

##### reduce(identity, accumulator)

Performs a reduction operation using the provided `identity` object as initial value and the accumulator function and returns the reduced value.

##### reduce(accumulator)

Performs a reduction operation using the first element of the stream as as initial value and the accumulator function and returns the reduced value wrapped as `Optional`.

##### groupingBy(keyMapper)

Groups all elements of the stream by applying the given keyMapper function and returns an object map, assigning an array value for each key.

Alias: `groupBy`

##### toMap(keyMapper, mergeFunction)

Groups all elements of the stream by applying the given keyMapper function and returns an object map, assigning a single value for each key. Multiple values for the same key will be merged using the given merge function.

Alias: `indexBy`

##### partitioningBy(predicate)

Groups all elements of the stream by the results of applying the given predicate to each element of the stream, returning an object with two keys `true` and `false`.

Alias: `partitionBy`

##### partitioningBy(size)

Groups all elements of the stream by chunks of the given size, returning an array of arrays.

Alias: `partitionBy`

##### joining(options)

Joins all elements of the stream into a string, using the following non-required options: `options.delimiter`, `options.prefix`, `options.suffix`.

Alias: `join`

##### iterator()

Returns a `StreamIterator` to traverse upon the elements described by this stream. `StreamIterator` defines a single method `next`, returning an object holding the next `value` and a boolean flag `done` indicating if the iterator has been finished.

```js
var iterator = stream.iterator(), result;
while (true) {
   result = iterator.next();
   console.log(result.value);
   if (result.done) {
      break;
   }
}
```

## Stream.Optional

Wraps a single value which may be `null` or `undefined`.

##### Optional.of(value)

Creates a new optional wrapper for the given non-null and non-undefined value.

##### Optional.ofNullable(value)

Creates a new optional wrapper for the given value. The value may be null or undefined.

##### Optional.empty()

Creates a new empty optional wrapper (same as `Optional.ofNullable(null)`).

##### get()

Returns the value if a value is present, otherwise throws an error.

##### isPresent()

Check if a value is present.

##### ifPresent(consumer)

Invoke the given consumer function for the specified value if present.

##### orElse(other)

Returns the value if present, otherwise return the given `other` value.

##### orElseGet(supplier)

Returns the value if present, otherwise return the result of invoking the supplier function.

##### orElseThrow(error)

Returns the value if present, otherwise throw the given error.

##### filter(predicate)

If a value is present and value matches the given predicate function, returns this optional, otherwise return an empty optional.

##### map(mappingFn)

If a value is present apply the given mapping function and wrap the resulting value with an optional.

##### flatMap(mappingFn)

If a value is present apply the given optional-returning mapping function, and return the optional result or empty.