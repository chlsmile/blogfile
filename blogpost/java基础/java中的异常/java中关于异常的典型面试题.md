## java中关于异常的典型面试题

### 面试题一

```java

public class Test {

    public int testException(){
        try{

            System.out.println("try block");
            System.exit(0);
        }catch (Exception e) {
            System.out.println("catch block");
        }finally{
            System.out.println("finally block");
        }
        return 0;
    }

    public static void main(String[] args) {
        Test t=new Test();
        System.out.println(t.testException());
    }
}

```



### 面试题二

```java

public class Test {

    public int testException() {
        try {
            return 0;
        } catch (Exception e) {
            System.out.println("catch block");
        } finally {
            System.out.println("finally block");
        }
        return 1;

    }

    public static void main(String[] args) {
        Test t = new Test();
        System.out.println(t.testException());

    }

}

```