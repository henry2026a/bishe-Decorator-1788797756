# 设计模式之装饰器 Decorator

> **发布时间**: 2026-09-03
> **标签**: 无

---

## 📞 联系方式
> 💬 **微信：sen232sen** | 🚀 **专业定制各类管理系统** | ⭐ **源码获取/技术支持**

---

在原本的东西的基础之上加上一层装饰  
当需要在原来的类上进行包装的时候，按照传统的方式需要一层层的继承，这样显然不方便。

  * 装饰器是继承的有力补充，比继承灵活，在不改变原有对象的情况下，动态的给一个对象扩展功能，即插即用
  * 通过使用不用装饰类及这些装饰类的排列组合，可以实现不同效果
  * 装饰器模式完全遵守开闭原则

其主要缺点是：装饰器模式会增加许多子类，过度使用会增加程序得复杂性。  
装饰器设计模式的必备要素：

  1. 抽象构件（Component）角色：定义一个抽象接口以规范准备接收附加责任的对象。
  2. 具体构件（ConcreteComponent）角色：实现抽象构件，通过装饰角色为其添加一些职责。
  3. 抽象装饰（Decorator）角色：继承抽象构件，并包含具体构件的实例，可以通过其子类扩展具体构件的功能。
  4. 具体装饰（ConcreteDecorator）角色：实现抽象装饰的相关方法，并给具体构件对象添加附加的责任。

下面我们看一下代码实现：  
首先，需要定义一个抽象构件，即接口，这里面要放我们想要实现的方法规范

    public interface Animal {
        void getDesc();
    
        void getPrice();
    }

然后 定义一个具体构件，实现抽象构件，在之后我们通过装饰器来装饰具体构件

    public class Cat implements Animal{
    
        @Override
        public void getDesc() {
            System.out.println("这是猫！");
        }
    
        @Override
        public void getPrice() {
            System.out.println("不要钱");
        }
    }

定义抽象的装饰器，这里持有抽象构件的引用，并通过构造器传入引用，这样达到增强的作用

    public abstract class Decorator implements Animal{
        protected Animal animal;
    
        public Decorator(Animal animal){
            this.animal = animal;
        }
        @Override
        public void getDesc() {
            animal.getDesc();
            System.out.println("加了装饰的猫");
        }
    
        @Override
        public void getPrice() {
            animal.getPrice();
            System.out.println("3块钱");
        }
    }

可以看到，在以上代码中，我们赋予了引用具体的对象。并且在实现抽象构件的方法中，调用了我们传入的对象的方法，并且在这之后去做一些其他的功能，这样就达到了不修改代码，对原来的功能进行增强的目的

最后，我们看一下具体的构件装饰器

    public class WhiteCatDecorator extends Decorator{
        public WhiteCatDecorator(Animal animal) {
            super(animal);
        }
    
        @Override
        public void getPrice() {
            super.getPrice();
            System.out.println("20块钱");
        }
    
        @Override
        public void getDesc() {
            super.getDesc();
            System.out.println("这是白猫");
        }
    }

具体的逻辑就是提供构造器入口赋值，然后对原来的方法进行增强

---

![sensen](images/sensen.png)
