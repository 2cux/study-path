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
