
## java基础知识

  - ### java语言特性

    1. java 采用 **Unicode** 编码格式

    2. **0x** 开头表示 **16进制** ，**0** 开头表示 **8进制**

    3. 这种形式表示的是 `char` 的二进制值，即该字符的编码值

      ```java
        char a = 0xffff;
      ```
    4. java的 `Random` 类的构造函数有两种，带种子和不带种子

      不带种子:
        ```java
          java.uitl.Random random = new java.util.Random();
        ```
        这种方式返回的随机数，每次运行结果都不一样

        带种子：
        ```java
        java.util.Random random = new java.util.Random(10);
        ```
        这种方式生成的随机数，返回结果是固定的，**每次运行结果是固定的，生成的随机序列也是固定的，当种子不同，生成的随机序列则不同**

        在java中主要通过 `Math.random()` 方法和 `Random` 类获得随机数，这两种方式获取随机数的方式是相同的，通过查看 `Math.random()` 方法的代码可以知道，  `Math.random()` 也是通过生成一个 `Random` 的实例，然后调用 `nextDouble()` 方法获取随机数
        ```java
        public static double random() {
          return RandomNumberGeneratorHolder.randomNumberGenerator.nextDouble();
        }
        //randomNumberGenerator 为一个Random类实例

        private static final class RandomNumberGeneratorHolder {
          static final Random randomNumberGenerator = new Random();
        }

        ```

        在Java中，随机数的产生取决于种子，随机数和种子之间的关系遵循以下两个规则：

          1. 种子不同，产生不同的随机数。

          2. 种子相同，即使实例不同也产生相同的随机数。

      `Random`类的默认种子（无参构造）是`System.nanoTime()`的返回值（JDK1.5版本以前默认种子是`System.currentTimeMillis()`的返回值），这个值是距离某一个固定时间点的纳秒数，不同操作系统和硬件有不同的固定时间点，也就是不同的操作系统纳秒值是不同的，而同一操作系统的纳秒值也会不同，随机数自然也就不同了

      ```java
      //Random 无参构造函数
      public Random() {
        this(seedUniquifier() ^ System.nanoTime());
      }
      ```
   5. fds
   6. fd
   7. fd
