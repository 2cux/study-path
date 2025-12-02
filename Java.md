# java的学习


## 利用泛型方法实现多数据类型的swap(2025.12.2)
```
import java.util.Arrays;
public class Swap {
    //定义一个泛型方法，可以交换任何类型的数据
    public static <T> void swap(T[] t,int i , int j){
        T temp = t[i];
        t[i] = t[j];
        t[j] = temp;
    }

    public static void main(String[] args) {
        //交换字符串类型
        String[] str = {"a", "b","c"};
        Swap.swap(str,0,1);
        System.out.println(Arrays.toString(str));

        //交换整形类型
        Integer[] in = {1,3,5};
        Swap.swap(in, 0, 1);
        System.out.println(Arrays.toString(in));
    }
}
```

## 利用多态(接口类)实现USB接口的功能(2025.11.28)
代码如下：
```
interface USB{
    void connect();
}

class Mouse implements USB{
    @Override
    public void connect(){
        System.out.println("鼠标被激活");
    }
}

class Keyboard implements USB{
    @Override
    public void connect(){
        System.out.println("键盘被激活");
    }
}

public class Computer {
    public static void main(String[] args){
        USB u1 = new Mouse();
        u1.connect();
        USB u2 = new Keyboard();
        u2.connect();
    }
}
```

## 利用多态(抽象类父类)实现辨别动物(2025.11.28)
代码如下：
```
abstract class Animal{
    //普通方法，每个人都一样，直接写
    public void sleep(){
        System.out.println("睡觉");
    }

    //抽象方法,因为你是抽象的，所以你不能被定义
    public abstract void bark();
}

//定义狗类
class Dog extends Animal{
    @Override
    public void bark() {
        System.out.println("汪汪汪！");
    }
}

//定义猫类
class Cat extends Animal{
    @Override
    public void bark() {
        System.out.println("喵喵喵！");
    }
}
public class Bark {
    public static void main(String[] args){
        //多态
        Animal a1 = new Dog();
        a1.bark();
        Animal a2 = new Cat();
        a2.bark();
    }
}
```

## 利用单例类实现唯一的皇帝（2025.11.28）
代码如下:
```
public class Emperor {
    private static final Emperor instance = new Emperor();//构造私有的唯一对象

private Emperor(){

    }//私有的构造方法
    public static Emperor getInstance(){
        return instance;
    }
}

class Test{
    public static void main(String[] args){
        Emperor e1 = Emperor.getInstance();
        Emperor e2 = Emperor.getInstance();
        System.out.println(e1 == e2);//输出true
    }
}
```

## 利用多态(普通类父类)实现多种支付方式(面向对象)（2025.11.27）
代码如下：
```
class Payment {
    public void pay(double money) {
        System.out.println("支付了xxx元");
    }
}

class WechatPay extends Payment{
    @Override
    public void pay(double money){
        System.out.println("微信支付" + money + "元");
    }
}

class AliPay extends Payment{
    @Override
    public void pay(double money){
        System.out.println("支付宝支付" + money + "元");
    }
}

class BankCardPay extends Payment{
    @Override
    public void pay(double money){
        System.out.println("银行卡支付" + money + "元");
    }
}

public class Shop {
//这里写Payment p是利用了多态，给子类退级操作，只要父类的pay方法
    public static void checkout (Payment p ,double money){
        p.pay(money);
    }
    public static void main(String[] args) {
        Payment p1 = new WechatPay();
        checkout(p1,100);

        Payment p2 = new AliPay();
        checkout(p2,200);

        Payment p3 = new BankCardPay();
        checkout(p3,300);
    }
}
```
