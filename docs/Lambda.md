### Lambda

#####语法

- 无参,无返回值
 ```text
    Runnable runnable = () -> System.out.println("Hello");
```

- 一个参数时 小括号可以省略
```text
Consumer<String> consumer = param -> System.out.println("param = " + param);
```

- 两个参数时 并且有返回值(当Lambda体只有一条语句时,return可以省略)
```text

 BinaryOperator<Long> binaryOperator = (x, y) -> {
            System.out.println("x = " + x);
            System.out.println("y = " + y);
            return x * y;
        };

 BinaryOperator<Long> binaryOperator = (x, y) -> x * y;

```

