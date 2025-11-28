# java的学习


## 1.利用多态实现多种支付方式(面向对象)
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


## 2.利用单利类实现唯一的皇帝
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
