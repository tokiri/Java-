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

    答：Exception是java程序运行中可预料的异常情况，咱们可以获取到这种异常，并且对这种异常进行业务外的处理。
    Error是java程序运行中不可预料的异常情况，这种异常发生以后，会直接导致JVM不可处理或者不可恢复的情况。所以这种异常不可能抓取到，比如OutOfMemoryError、NoClassDefFoundError等。
    其中的Exception又分为检查性异常和非检查性异常。两个根本的区别在于，检查性异常 必须在编写代码时，使用try catch捕获（比如：IOException异常）。非检查性异常 在代码编写使，可以忽略捕获操作（比如：ArrayIndexOutOfBoundsException），这种异常是在代码编写或者使用过程中通过规范可以避免发生的。
    
>4. sleep(),wait(),yield(),interrupt()的区别

    答：
    1）sleep：在指定的毫秒数内让当前正在执行的线程休眠（进入阻塞状态），锁未被释放，其他线程无法分配到该线程调用的资源。 
    2）wait：调用wait使线程挂起（进入阻塞状态，锁被释放），直到线程得到了notify或notifyAll消息，线程才会进入就绪状态，其他线程可以被分配到资源。
    3）yield：如果知道已经完成了所需要的工作，就可以给线程调度一个机制暗示（进入就绪状态），锁未释放，但是相同优先级的可获得资源。
    4）interrupt：设置当前线程中断标记为true。
    sleep和yield的区别：
    1）sleep()方法给其他线程运行机会时不考虑线程的优先级,因此会给低优先级的线程以运行的机会
    2）yield()方法只会给相同优先级或更高优先级的线程以运行的机会
    3）线程执行sleep()方法后转入阻塞(blocked)状态,而执行yield()方法后转入就绪(ready)状态
    4）sleep()方法声明会抛出InterruptedException,而yield()方法没有声明任何异常
    5）sleep()方法比yield()方法具有更好的移植性(跟操作系统CPU调度相关)

    
