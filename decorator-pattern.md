# 装饰模式

## 装饰模式概述

### 定义

> 动态的给一个对象增加一些额外的职责。就扩展功能而言，装饰模式提供了一种比使用子类更加灵活的替代方案。

## 装饰模式结构与实现

### 装饰模式结构

1. Component（抽象构件）：它是具体构件和抽象装饰类的共同父类，声明了在具体构件中是实现的业务方法，它的引入可以是客户端以一致的方式处理未被装饰的对象以及装饰之后的对象，实现客户端的透明操作。
2. Concrete Component（具体构件）：他是抽象构件类的子类，用于定义具体的构件对象，实现了在抽象构件中声明的方法，装饰类可以给它增加额外的职责（方法）
3. Decorator（抽象装饰类）：它也是抽象构件类的子类，用于给具体构件增加职责，但是具体职责在其子类中实现。它维护一个指向抽象构件对象的引用，通过该引用可以调用装饰之前构件对象的方法，并通过其子类扩展该方法，以达到装饰的目的。
4. Concrete Decorator（具体装饰类）：它是抽象装饰类的子类，负责向构件添加新的职责。每一个具体装饰类都定义了一些新的行为，它可以调用在抽象装饰类中定义的方法，并可以增加新的方法用于扩充对象的行为。

## 装饰模式实现

1. 抽象构建类代码如下：

```java
public abstract class Component{
    public abstract void operation();
}
```

2. 具体构件类代码如下：

```java
public class ConcreteComponent extends Component{
    public void operation(){
        // 基本功能的实现
    }
}
```

3. 抽象装饰类代码如下（核心）：

```java
public class Decotator extends Component{
    private Component component; // 维持一个对抽象化构件对象的引用
    
    // 注入一个抽象构件类型的对象
    public Decotator(Component component){
        this.component = component;
    }
    
    public void operation(){
        component.operation(); // 调用原有业务方法
    }
    
}
```

4. 具体装饰类代码如下：

```java
public class ConcreteDecotator extends Decorator{
    
    public ConcreteDecorator(Component component){
        super(component);
    }
    
    public void operation(){
        super.operation(); // 调用原有业务方法
        addedBehavior(); // 调用新增业务方法
    }
    
    public void addedBehavior(){
        // 新增业务方法
    }
}
```

