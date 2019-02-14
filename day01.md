>1. int 和 integer 的区别？
  
    答：integer是int的包装类，主要是为了能够将基本数据类型当成对象操作。
    
```java

//自动装箱机制
class AutoUnboxingTest {
 
    public static void main(String[] args) {
        Integer a = new Integer(3);
        Integer b = 3;                  // 将3自动装箱成Integer类型
        int c = 3;
        System.out.println(a == b);     // false 两个引用没有引用同一对象
        System.out.println(a == c);     // true a自动拆箱成int类型再和c比较
    }
}

//自动拆箱机制
public class Test03 {
 
    public static void main(String[] args) {
        Integer f1 = 100, f2 = 100, f3 = 150, f4 = 150;
 
        System.out.println(f1 == f2);   //true 在int的范围内会直接引用常量池中的Integer的对象
        System.out.println(f3 == f4);   //false 不在int的范围内（-128~127）会new新的Integer对象
    }
}
```
    
    
