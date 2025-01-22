---
title: "Java 代码片段"
description: "Java 单例模式，工厂模式，延迟初始化，异常处理，Builder 模式"
pubDate: "Jul 08 2022"
heroImage: "/blog-placeholder-3.jpg"
---

Java 有不少经典的代码片段和设计模式，常用于解决常见的问题或提升代码的可读性和效率。以下是几个经典的 Java 代码片段：

### 1. 单例模式 (Singleton Pattern)

确保一个类只有一个实例，并提供全局访问点。

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### 2. 工厂模式 (Factory Pattern)

用于根据条件动态创建实例，而不需要指定类的具体类型。

```java
public interface Product {
    void create();
}

public class ConcreteProductA implements Product {
    public void create() {
        System.out.println("Product A created");
    }
}

public class ConcreteProductB implements Product {
    public void create() {
        System.out.println("Product B created");
    }
}

public class Factory {
    public static Product getProduct(String type) {
        if (type.equals("A")) {
            return new ConcreteProductA();
        } else if (type.equals("B")) {
            return new ConcreteProductB();
        }
        return null;
    }
}
```

### 3. 延迟初始化 (Lazy Initialization)

用于在首次需要时才初始化资源，提升程序的效率。

```java
public class LazyLoadedClass {
    private static LazyLoadedClass instance;

    private LazyLoadedClass() {}

    public static LazyLoadedClass getInstance() {
        if (instance == null) {
            instance = new LazyLoadedClass();
        }
        return instance;
    }
}
```

### 4. 异常处理的 try-with-resources

Java 7 引入的资源管理方式，用于自动关闭资源（如文件、网络连接等）。

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### 5. Builder 模式

用于简化复杂对象的构建过程。

```java
public class Car {
    private String color;
    private String engine;
    private int seats;

    public static class Builder {
        private String color;
        private String engine;
        private int seats;

        public Builder setColor(String color) {
            this.color = color;
            return this;
        }

        public Builder setEngine(String engine) {
            this.engine = engine;
            return this;
        }

        public Builder setSeats(int seats) {
            this.seats = seats;
            return this;
        }

        public Car build() {
            Car car = new Car();
            car.color = this.color;
            car.engine = this.engine;
            car.seats = this.seats;
            return car;
        }
    }
}
```

这些经典的代码片段不仅便于代码复用，也符合 Java 的设计模式和最佳实践，便于团队维护和扩展代码。
