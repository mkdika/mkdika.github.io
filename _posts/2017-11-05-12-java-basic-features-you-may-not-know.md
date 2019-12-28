---
layout      : post
title       : "12 Java Basic Features You May not Know"
date        : 2017-11-05 18:00:00 +0700
categories  : Java
tags        : [java, oca]
comments    : true
---
![Imgur](https://i.imgur.com/sDrqQW3.png)

Recently I took the Oracle Certified Associate Java Programmer 8 (OCAJP). Even has been become
a Java programmer for many years, there are still several new things, especially the detail things
or the standard term about Java basic features which was I just know. Some of those may happened
because I rarely did the systematically and elaborate learning before, I just learn by practice, or
some features are not frequently used too.

This post is intended for beginner to intermediate programmer in Java. As you are going to know
something basic yet useful to implement into your code or comprehension. If you are experienced
Java programmer, feel free to skip it.

I have summarized into 12 sections, with explanation for each section. Please note that all code are
test within JDK 8.

## 1. Initializer Block & Initialization Order

There're `static` and `non-static` initializer block. The block of code which will be execute
while creating instance of the object, before the `constructor` blocks be executed.

The `non-static` initializer block is look like this:

```java
{
  // this is non-static initializer block code
}
// the rest of code, the constructor, instance variables, methods, etc.
```

The `static` initializer block is look like this:

```java
static{
  // this is static initializer block code
}
// the rest of code, the constructor, instance variables, methods, etc.
```

So, while you instance a new object, the initialization order (execution) will be:

1. Static variable direct assignment.
2. Static initializer block.
3. Instance variable direct assignment.
4. Non-static initializer block.
5. Constructors.

## 2. Logical Operators

Java have 2 kind of logical operator, the `short-circuiting` and `not short-circuting`.

|       Operator       | Meaning       | Note                 |
| :------------------: | ------------- | -------------------- |
|       `a && b`       | Logical `AND` | Short-Circuiting     |
| `a` &#124;&#124; `b` | Logical `OR`  | Short-Circuiting     |
|       `a & b`        | Logical `AND` | Not Short-Circuiting |
|    `a` &#124; `b`    | Logical `OR`  | Not Short-Circuiting |

For `not short-circuiting` operator, both left and right side operant will be evaluate (execute).
Conversely, for `short-circuiting` operator, dont evaluate the right side operant if it isnt necessary.

Example, for `&&` operator, if the left side is `false`, it will skip to evaluate the right side.
As well as, for `||` operator, if the left side is `true`, it will skip to evaluate the right side.

Take a look at example below:

```java
class ShortCircuiting {
    public static void main(String[] args) {
        System.out.println("Not Short-Circuiting AND.");
        if (leftSide(false) & rightSide(true)) {}
        System.out.println("Not Short-Circuiting OR.");
        if (leftSide(true) | rightSide(false)) {}
        System.out.println("Short-Circuiting AND.");
        if (leftSide(false) && rightSide(true)) {}
        System.out.println("Short-Circuiting OR.");
        if (leftSide(true) || rightSide(false)) {}
    }

    static boolean leftSide(boolean b) {
        System.out.println("Left executed!");
        return b;
    }

    static boolean rightSide(boolean b) {
        System.out.println("Right executed!");
        return b;
    }
}
```

And the result is going to be:

```bash
Not Short-Circuiting AND.
Left executed!
Right executed!
Not Short-Circuiting OR.
Left executed!
Right executed!
Short-Circuiting AND.
Left executed!
Short-Circuiting OR.
Left executed!
```

As shown above, the `short-circuiting` operator just evaluated the left side operand when the right
side does not necessary.

## 3. Integer Wrapper Cache Implementation (Cache)

Integer cache implementation is the feature since Java 5. It's related to memory efficient and
performance improvement for Integer type object handling. Integer objects are cached internally
and reused via the same referenced objects. The rules are:

- Applicable for Integer values in range between –127 to +127.
- This Integer caching works only on auto-boxing. Integer objects will not be cached when they are
  built using the constructor.
- This auto-boxing is also similar, if we're using the `valueOf` method.

Is all of the rules above applied, then Integer will be cache.

```java
class PrimitiveWrapper {
    public static void main(String[] args) {
        Integer a = 127;    // auto-boxing
        Integer b = Integer.valueOf(127);   // supported
        System.out.println((a == b));   // true
        Integer c = 200;    // out-of cache range
        Integer d = 200;    // out-of cache range
        System.out.println((c == d));   // false
        Integer e = new Integer(100);   // use constructor
        Integer f = new Integer(100);   // use constructor
        System.out.println((e == f));   // false
    }
}
```

## 4. Checked & Unchecked Exception

![Imgur](https://i.imgur.com/tzcWU0Z.png)

There are 2 kind of exceptions in Java, the checked and un-checked exception. The super class of all
exception class in Java is `java.lang.Throwable`. It also have 3 different purpose sub-classes.

1. `java.lang.Exception`, is categorized as **checked** exception, and their sub-classes.
2. `java.lang.RuntimeException`, is categorized as **un-checked** exception, and their sub-classes.
3. `java.lang.Error`, is categorized as **un-checked** exception, and their sub-classes.

The checked exception are the exceptions that need to be handled, `try ... catch ... finally` or
`throws` statement on method/constructor header. Conversetly, it no need for un-checked exceptions.

## 5. Covariant Return Type

The covariant return type is the return type that may vary in the same direction as the subclass. So,
it is possible to override method by changing the return type as long as it is not primitive type and
its wrapper class, moreover it should be the sub-class type.

Take a look at example below:

```java
class A {
    A get() { return this; }
    Integer calculate(int i) { return i; }
}

class B extends A {
    B get() { return this; } // covariant return type
    Byte calculate(int i) { return 1; } // this will cause compile error.
}

class C extends B {
    C get() { return this; } // covariant return type
}
```

## 6. Multi-Dimensional Array Initialization

When we initialize a multi-dimensional array, it only necessary for us to define the first dimension
size and left the rest of others size initialize as needed (`1+n`). For instance, we usually define
a two dimensional array like this:

```java
int[][] arr = new int[4][4]; // define all dimension size
```

Actually it is equivalent to something like this:

```java
int[][] arr = new int[4][]; // only define first dimension size
arr[0] = new int[4];
arr[1] = new int[4];
arr[2] = new int[4];
arr[3] = new int[4];
```

Further more, we can define different array size for `1+n` dimension. Take a look at the example below:

```java
class ArrayDemo {
    public static void main(String[] args) {
        int[][] arr = new int[4][]; // only define first dimension size
        arr[0] = new int[2];
        arr[1] = new int[3];
        arr[2] = new int[4];
        arr[3] = new int[5];
        System.out.println(Arrays.deepToString(arr));
    }
}
```

And the output:

```bash
[[0, 0], [0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0, 0]]
```

**Bonus:**

All of these are valid way to define the empty two dimensional array.

```java
int[][] a = {{}};
int[] b[] = {{}};
int c[][] = {{}};
```

## 7. Access Modifier Hierarchy on Method Overriding.

![Imgur](https://i.imgur.com/4k8Wa9M.jpg)

Java Access Modifier Hierarchy, from the most isolated are `private` -> `<default>` -> `protected` ->
`public`. Except for `private` access modifier, because the resources only can be access from inside
the class or its inner class. For the others, when overriding methods, the access modifier level must
be same or at higher hierarchy.

```java
class TestA {
     protected void printSomething() {}
}

class TestB extends TestA{
    void printSomething(){} // this default access modifier will cause error.
}
```

The `TestB` class will have compile time error cause of downgraded access modifier on method
`printSomething`. We can solve this by change its access modifier to `protected` or `public`.

## 8. StringBuffer vs StringBuilder

Basically, `StringBuffer` methods are `synchronize`, while `StringBuilder` are not. `StringBuilder` is
the commonly use, unless we really are trying to share a buffer between threads, cause using
synchronized methods in a single thread is overkill. From performance perspective, `StringBuilder`
is relatively faster than `StringBuffer` because of not `synchronized`. Take a look at example
classes below and the result, that run separately on same machine.

```java
class StringBufferDemo {
    public static void main(String[] args) {
        long t1 = System.currentTimeMillis();
        StringBuffer sb = new StringBuffer(10_000_000);
        for (int i =0;i<10_000_000;i++) {
            sb.append(randInt(1, 1000));
        }
        long t2 = System.currentTimeMillis();
        System.out.println("StringBuffer Done! "+(t2-t1)+" msecs.");
    }
    static int randInt(int min, int max) {
        return ((int) (Math.random() * ((max - min) + 1)) + min);
    }
}
```

```java
// Output:
StringBuffer Done! 521 msecs.
```

```java
class StringBuilderDemo {
    public static void main(String[] args) {
        long t1 = System.currentTimeMillis();
        StringBuilder sb = new StringBuilder(10_000_000);
        for (int i =0;i<10_000_000;i++) {
            sb.append(randInt(1, 1000));
        }
        long t2 = System.currentTimeMillis();
        System.out.println("StringBuilder Done! "+(t2-t1)+" msecs.");
    }
    static int randInt(int min, int max) {
        return ((int) (Math.random() * ((max - min) + 1)) + min);
    }
}
```

```java
// Output:
StringBuilder Done! 378 msecs.
```

Base on each output, `StringBuilder` seems faster than `StringBuffer`.

## 9. Numeric Wrapper Literal Assignment Behaviour

The numeric wrapper class `Byte`,`Short`,`Integer`,`Long`,`Float`,`Double` can be assigned to value
literally because of `auto-boxing` features. But it have different interpretation from its primitive one.

For integer number type wrapper, it only apply to `Byte`,`Short`,`Integer`. And for floating number
type wrapper only accept fractional value to `Double`, unless we use literal type suffix
(`L`,`F`,`D`).

```java
class AutoBoxingRule {
    public static void main(String[] args) {
        // Primitive type assignment
        byte pb = 10;
        short ps = 10;
        int pi = 10;
        long pl = 10;

        float pf = 10;
        double pd = 10;
        float pf2 = 2.5; // COMPILE ERROR
        double pd2 = 2.5;

        // Wrapper type assignment
        Byte wb = 10;
        Short ws = 10;
        Integer wi = 10;
        Long wl = 10; // COMPILE ERROR

        Float wf = 10;  // COMPILE ERROR
        Double wd = 10; // COMPILE ERROR
        Float Wf2 = 2.56; // COMPILE ERROR
        Double wd2 = 2.5;
    }
}
```

## 10. Type Casting

![Imgur](https://i.imgur.com/7GCb5I1.png)

Type Casting is when we assigning a value of one type to a variable of another type.

```java
int x = 10;
byte y = (byte)x;
```

As above example, We have a `x` variable which is `int` type, then assigned to `y` which is `byte`
type.

There are 2 kind of Type Casting:

1. **Implicit Cast (Widening Casting)**,
  It take place when two types are compatible or the target type is larger than the source type. In
  object reference type, the target type (reference class) should be the super-classes or higher
  hierarchy from the source type (object reference).

2. **Explicit Cast (Narrowing Casting)**,
  It happen when assign the larger type value to a variable of smaller type. In object reference type,
  the source type should be the one that have been assigned with object reference of same class or
  its lower hierarchy.

Take a look at example classes below:

```java
class A {}

class B extends A{}

class C extends B{}

class D extends A{}

class Main {
    public static void main(String[] args) {
        A a = new B(); // Implicit Casting (Widening)
        B b = (B) a; // Explicit Casting (Narrowing) , same class object reference
        A a1 = new C(); // Implicit Casting (Widening)
        B b1 = (C)a1; // Explicit Casting (Narrowing), from lower hierarchy
        A a2 = new D(); // Implicit Casting (Widening)
        B b2 = (B) a2; // This will cause java.lang.ClassCastException
    }
}
```

The last line will cause `RuntimeException` because of `class D cannot be cast to B`. These casting
behaviour apply for `interface` and its `implements` classes as well.

## 11. Passing by Value & Reference

When we pass the primitive data type variable to method, it actually pass the value only, and it will
create another local variable within the methods, this is called Pass by Value.

This behaviour also apply when you pass `String` and other Wrapper Class (`Integer`,`Double`, etc) variable, you will pass the reference, but since they are immutable object, when you manipulate the
value, it will create a new reference object instead of manipulate the existing one. But for mutable
object it will pass the reference, and these are called Pass by Reference.

Take a look at the code example below and its output.

```java
class PassParam {
    public static void main(String[] args) {
        // Primitive type pass the value
        int x = 100;
        System.out.println(x); // 100
        passInt(x);
        System.out.println(x); // 100

        // pass the reference but immutable
        Integer i = 1000;
        System.out.println(i); // 1000
        passInteger(i);
        System.out.println(i); // 1000

        // pass the reference but immutable
        String s = "boo";
        System.out.println(s); // boo
        passString(s);
        System.out.println(s); // boo

        // pass the reference and mutable object
        RefMe me = new RefMe("Mix");
        System.out.println(me); // Mix
        passReference(me);
        System.out.println(me); // Max
    }

    static void passInt(int n) { n = 200; }
    static void passInteger(Integer n) { n = 2000; }
    static void passString(String s) { s = "foo"; }
    static void passRef(RefMe me) { me.setName("Max"); }
}

class RefMe {
    String name;
    RefMe(String name) {
        this.name = name;
    }
    void setName(String name) {
        this.name = name;
    }
    public String toString() { return name;}
}
```

## 12. Numeric Promotion

![Imgur](https://i.imgur.com/rVX9KBJ.png)

Numeric Promotion is the conversion of a smaller numeric type into a larger numeric type implicitly.

The Numeric Promotion rules:

1. If two values have different data types, it will automatically promote one of the values to the
  **larger of the two data types**.
2. If one of the values is integral and the other is floating-point, it will automatically promote
  **the integral value to the floating-point value's** data type.
3. Smaller data type, `byte`, `short` and `char`, are first **promoted to `int`** any time they are
  used with a Java binary arithmetic operator, even if neither of the operands is `int`.
4. The resulting value will have the same data type as its promoted operands.

Take a look at these cases.

**Case-1: i * l** , `long` is larger than `int`, so `int` value is promoted to `long`, and resulting
value is `long`.

```java
int i = 2;
long l = 5;
```

**Case-2: d + f** , `double` is larger than `float`, so `float` value is promoted to `double`, and
resulting value is `double`.

```java
double d = 2.5;
float f = 1.5f;
```

**Case-3: x / y** , both will promoted to `int` before operation, and resulting value is `int` (not `double`).

```java
short x = 3;
short y = 5;
```

**Case-4: a * b / c** , first `a` will promoted to `int` because of `short`, then `a` will be promoted
to `float` so it can be multiplied with `b`. The result of `a` * `b` will automatically promoted to
`double`, so it can be divide with `c`, and resulting value is `double`.

```java
short a = 8;
float b = 6;
double c = 5;
```

Furthermore about Java Conversions and Promotions, please visit this
[page](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html){:target="_blank"}.

Now we are reach the end of this post. These 12 list are based on my experience and observation, of
course there are still plenty of Java platform features, keep exploring.

I hope you enjoy and found something useful.
