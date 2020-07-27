# Java Randomness
In this note, I'll briefly cover some of the most used random capabilities in Java. And we may cover some bonuses in JS. 

## Class Random
[Class Random](https://docs.oracle.com/javase/8/docs/api/java/util/Random.html)

```
public class Random
extends Object
implements Serializable
```

**Many applications will find the method `Math.random()` simpler to use.**

### Constructor
* `Random()`: Creates a new random number generator.
* `Random(long seed)`: Creates a new random number generator using a single long seed.

### Methods
* Streams
    - `DoubleStream	doubles()/` 4 variations
    - `IntStream ints()` 4 variations
    - `LongStream longs()` 4 variations
* next
    - `protected int next(int bits)`
    - `boolean	nextBoolean()`
    - `void	nextBytes(byte[] bytes)`
    - `double nextDouble()`
    - `float nextFloat()`
    - `int nextInt()`
    - `long nextLong()`
    - `double nextGaussian()`: Returns the next pseudorandom, Gaussian ("normally") distributed double value with mean 0.0 and standard deviation 1.0 from this random number generator's sequence.
* `void	setSeed(long seed)`

## Math.random()
`public static double random()`: Returns a double value with a positive sign, greater than or equal to 0.0 and less than 1.0. Returned values are chosen pseudorandomly with (approximately) uniform distribution from that range. https://docs.oracle.com/javase/8/docs/api/java/lang/Math.html#random--