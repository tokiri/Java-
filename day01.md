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

>2. 如何实现对象的克隆？

    答：可以使用两中方法实现
    1）实现Cloneable接口并重写Object类中的clone()方法；
    2）实现Serializable接口，通过对象的序列化和反序列化实现克隆，
```java
//通过实现Serializable，通过序列化和反序列化实现克隆

File file = new File("file"+File.separator+"out.txt");

    FileOutputStream fos = null;
    try {
        fos = new FileOutputStream(file);
        ObjectOutputStream oos = null;
        try {
            oos = new ObjectOutputStream(fos);
            Person person = new Person("tom", 22);
            // 调用 person的 tostring() 方法
            System.out.println(person);
            //写入对象
            oos.writeObject(person);            
            oos.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }finally{
            try {
                oos.close();
            } catch (IOException e) {
                System.out.println("oos关闭失败："+e.getMessage());
            }
        }
    } catch (FileNotFoundException e) {
        System.out.println("找不到文件："+e.getMessage());
    } finally{
        try {
            fos.close();
        } catch (IOException e) {
            System.out.println("fos关闭失败："+e.getMessage());
        }
    }

    FileInputStream fis = null;
    try {
        fis = new FileInputStream(file);
        ObjectInputStream ois = null;
        try {
            ois = new ObjectInputStream(fis);
            try {
                Person person = (Person)ois.readObject();   //读出对象
                System.out.println(person);
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            } 
            } catch (IOException e) {
              e.printStackTrace();
            }finally{
              try {
                  ois.close();
              } catch (IOException e) {
                System.out.println("ois关闭失败："+e.getMessage());
              }
        }
    } catch (FileNotFoundException e) {
        System.out.println("找不到文件："+e.getMessage());
    } finally{
        try {
            fis.close();
        } catch (IOException e) {
            System.out.println("fis关闭失败："+e.getMessage());
        }
    }

```

>3. Error和Exception有什么区别？

    
    
