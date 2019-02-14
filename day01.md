>1. int 和 integer 的区别？
  
    答：integer是int的包装类，主要是为了能够将基本数据类型当成对象操作。
    
    自动装箱机制
    
    class AutoUnboxingTest {
    public static void main(String[] args) {
    Integer a = new Integer(3);
    Integer b = 3;                  // 将3自动装箱成Integer类型
    int c = 3;
    System.out.println(a == b);     // false 两个引用没有引用同一对象
    System.out.println(a == c);     // true a自动拆箱成int类型再和c比较
    }
    }
    
    拆箱机制
    
