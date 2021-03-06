# 笔记四 Java面向对象对象的三大特性（B） 

[TOC]

## 1. 封装

> 含义：隐藏类的实现细节，让使用者只能通过程序员规定的方法来访问数据

###  1.1 访问控制符

> public  :   可以被同一个项目中所有类访问,具有项目可见性,这是**最大的访问权限**
>
> private ：成员变量和方法只能在**类内被访问**,具有类可见性.
>
> default ：成员变量和方法只能被**同一个包里**的类访问,具有包可见性
>
> protected ：可以被**同一个包中的类**访问,被同一个项目中**不同包中的子类访问**
>
>  

|   作用    | 同一类 | 子类 | package | 其他包 |
| :-------: | :----: | :--: | :-----: | :----: |
|  public   |   √    |  √   |    √    |   √    |
|  private  |   √    |  ✗   |    ✗    |   ✗    |
| protected |   √    |  √   |    √    |   ✗    |
|  default  |   √    |  ✗   |    √    |   ✗    |

```java
package note4.access;

/**
 * @author Calvin
 * @titile: 访问控制符
 * @date 2019/2/21
 * @since 1.0
 */
public class PrivateSymbol {

    /**
     * private 修饰的成员变量，只能适用于当前类
     */
    private String message = "PRIVATE_ACCESS_CONTROLLER_SYMBOL";

    /**
     * pirvate 修饰的方法，只能适用于当前类
     * @param message
     * @return
     */
    private void println(String message){
        System.out.println(message);
    };
}

// 跨类访问 -> 异常信息 -> prntln(java.lang.String)' has private access in 'note4.access.PrivateSymbol 
```

```java
package note4.access;

/**
 * @author Calvin
 * @titile: 受保护访问控制符
 * @date 2019/2/21
 * @since 1.0
 */
public class ProtectedSymbol {

    protected String message= "PROTECTED_ACCESS_CONTROLLER_SYMBOL";

    protected void println(String message){
        System.out.println(message);
    }
}

/**
 * 在同一个包下访问 protected
 */
class AccessProtectdBySamePackage{

    public static void main(String[] args) {
        /**
         * protected -> 可以被同一个包中的类访问
         */
        ProtectedSymbol protectedSymbol = new ProtectedSymbol();
        protectedSymbol.println(protectedSymbol.message);
    }
}

/**
 * 通过子类访问父类 protected
 */
class AccessProtectdByMyChild extends ProtectedSymbol {

    public static void main(String[] args) {
        /**
         * protected -> 可以通过子类访问父类 
         */
        ProtectedSymbol protectedSymbol = new ProtectedSymbol();
        protectedSymbol.println(protectedSymbol.message);
    }
}

// 在不同包访问Protected-> 异常报错信息 message' is not public in 'note4.access.ProtectedSymbol'. Cannot be accessed from outside package
```

```java
package note4.access;

/**
 * @author Calvin
 * @titile: 默认访问控制控制符
 * @date 2019/2/21
 * @since 1.0
 */
public class DefaultSymbol {

    String message= "DEFAULT_ACCESS_CONTROLLER_SYMBOL";

    void println(String message){
        System.out.println(message);
    }
}

/**
 * 在同一个包下访问 Default
 */
class AccessDefaultBySamePackage{

    public static void main(String[] args) {
        /**
         * default -> 可以被同一个包中的类访问
         */
        DefaultSymbol defaultSymbol = new DefaultSymbol();
        defaultSymbol.println(defaultSymbol.message);
    }
}

/**
 * 通过子类访问父类 default
 */
class AccessDefaultByMyChild extends DefaultSymbol {

    public static void main(String[] args) {
        /**
         * Default -> 可以通过子类访问父类
         */
        DefaultSymbol defaultSymbol = new DefaultSymbol();
        defaultSymbol.println(defaultSymbol.message);
    }
}

// 在不同包访问Default -> 异常报错信息 message' is not public in 'note4.access.DefaultSymbol'. Cannot be accessed from outside package
```

### 1.2 具体步骤

> 1.修改属性的可见性来限制对属性的访问
>
> 2.为每个属性创建一对赋值(setter)方法和取值(getter)方法，用于对这些属性的存取
>
> 3.在赋值方法中,加入对属性的存取控制语句

```java
package note4.access;

/**
 * @author Calvin
 * @titile: 访问控制符操作步骤
 * @date 2019/2/21
 * @since 1.0
 */
public class AccessSymbolOperation {

    // 修改属性的可见性来限制对属性的访问
    private String message;
    private String title;

    public AccessSymbolOperation(String message, String title) {
        this.message = message;
        this.title = title;
    }

    // 为每个属性创建一对赋值(setter)方法和取值(getter)方法，用于对这些属性的存取
    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        // 在赋值方法中,加入对属性的存取控制语句
        this.message = message;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }


}
```





##2. 继承

### 2.1 定义

>  a.子类继承父类属性和方法，但私有属性和私有方法不能继承
>
>  b.通过关键字 extends

###  2.2 作用

> 代码重用，代码复用

###  2.3 注意事项

> a. 一个类 -> 继承一个父类  (一个孩子只有一个父亲)
>
> b. 一个类 ->  多个子类  (一个父亲有多个孩子)
>
> c.  构造方法不继承
>
> d. 没有访问权限的成员不继承
>
> e. 静态成员不继承

```java
package note4.extend;

/**
 * @author Calvin
 * @titile: 父类
 * @date 2019/2/21
 * @since 1.0
 */
public class Father {

    /**
     *  基因
     */
    protected String gene;

    /**
     * 名称
     */
    private String name = "Calvin";

    /**
     * 健康身体
     */
    public void haveHealthBody(){
        System.out.println("HEALTH_BODY");
    }
}
```

```java
package note4.extend;

/**
 * @author Calvin
 * @titile:
 * @date 2019/2/21
 * @since 1.0
 */
public class Children extends Father{

    // 不能继承父类私有属性 name' has private access in 'note4.extend.Father'
    // private String name = super.name;

    /**
     * 继承父亲的基因
     */
    private String gene = super.gene;

    /**
     * 继承父类健康身体
     */
    private void extendFatherHealthBody(){
        super.haveHealthBody();
    }

}

```



## 3. 多态

### 3.1 定义

> 多态指的是**编译器（申明变量是）**和**运行期（创建对象后）**表现为**不同的形态（数据类型）**

### 3.2 注意事项

> a. 继承的存在(继承是多态的基础,没有继承就没有多态)
>
> b. 子类重写父类的方法(多态下调用子类重写的方法)
>
> c.  父类引用变量指向子类对象(子类到父类的类型转换)

### 3.3 子类转换成父类规则

> 1. 将一个**父类的引用指向一个子类**的对象,称为**向上转型(upcastiog)**,自动进行类型转换.
> 2. 此时通过**父类引用调用的方法是子类覆盖或继承父类的方法,不是父类的方法.**
> 3.  此时通过父类引用变量无法调用子类特有的方法
> 4. 如果父类要**调用子类的特有方法**就得将**一个指向子类对象的父类引用赋给一个子类的引用**,称为**向下转型**,**此时必须进行强制类型转换**



![1550720233279](C:\Users\Calvin\AppData\Roaming\Typora\typora-user-images\1550720233279.png)



```java

a.向上转型：父类 = 子类实例化() ========== 1.子类和父类确立关系 ============== 2.系统自动完成  作用：父类可以接受来自不同子类的实现方式（覆盖父类方法的子类方法）。  例如：B(fun1)、C(fun1) 继承 A (fun1) ====>> 如何子类如何获取覆盖fun1 =====>>fun(new B) || fun(new C)==========>> fun(A a){ a.fun1()}=========>>向上转型：子类可以获取到子类覆盖的对应方法。 


b.向下转型: 子类 = 父类实例化() ========== 1.无法确立关系，需要先进行确立关系（向上转型后）,才能进行转换。================== 否则，强制转换（转换异常）  作用：可以获取子类自定义的方法。


package note4.manystate;

/**
 * 父类
 */
public class Parent {

    /**
     * fun1()
     **/
    public void fun1() {
        System.out.println("【执行的是父类fun1】");
    }

    /**
     * fun2()
     **/
    public void fun2() {
        this.fun1();
    }
}

/**
 * 子类A继承父类
 */
class Children1 extends Parent {

    /**
     * 重载 -> 父类fun1()
     */
    @Override
    public void fun1() {
        System.out.println("【执行的是子类A fun1】");
    }

    /**
     * 自定义方法fun3
     */
    public void fun3() {
        System.out.println("【执行的是子类A fun3】");
    }
}

/**
 * 子类B继承父类
 */
class Children2 extends Parent {

    /**
     * 重载 -> 父类fun1()
     */
    @Override
    public void fun1() {
        System.out.println("【执行的是子类B fun1】");
    }

    /**
     * 自定义方法fun4
     */
    public void fun4() {
        System.out.println("【执行的是子类A fun4】");
    }
}


/**
 * Created by Calvin on 2018/6/5
 * 向上转型
 * 父类 = 子类实例化
 */
class Upcasting {

    public static void main(String[] args) {
        Children1 children = new Children1();
        Parent parent = children; // 向上转型：父类 = 子类实例化
        parent.fun1();            // 【执行的是子类A fun1】
    }
}


/**
 * Created by Calvin on 2018/6/5
 * 向下转型
 * 子类 = 父类实例化
 * ps:
 * 1.向下转型，必须先向上转型（确立父子关系），才能进行向下转型。
 * 2.如果单一的向下转型，报错：转换异常。
 */
class Downcasting {

    public static void main(String[] args) {

        Parent parent = new Children1();          // 向上转型（确立关系）
        Children1 children = (Children1) parent;  // 向下转型
        children.fun1();                          // 调用方法被复写 【执行的是子类A fun1】
        children.fun2();                          // 调用父类的方法 【执行的是父类fun1】
        children.fun3();                          // 调用子类自定义的方法 【执行的是子类A fun3】
    }
}


/**
 * Created by Calvin on 2018/6/6
 * 向上转型功能代码
 */
class PolymorphicFunction {

/********************************************* 不使用多态 ****************************/
    /**
     * 缺点: 每一拓展子类,每一次都fun()方法都要重载一次。
     * A==>>B,C,D
     */
    public void unUsedPolymorphic() {
        unfun(new Children1());
        unfun(new Children2());
    }

    public void unfun(Children1 children1) {
        children1.fun1();
    }

    public void unfun(Children2 children2) {
        children2.fun1();
    }

    /********** 使用多态: 实现父类下任意子类对象，并调用方法 ***********************/

    public void usePolymorphic() {
// 父类的通用方法 fun1 -> 只要向上转型实例其中一个子类 -> 就能获取到子类重载父类的方法 -> 使用的是子类的方法
        fun(new Children1());
        fun(new Children2());
    }

    public void fun(Parent parent) {
        parent.fun1();
    }
}

```




![](C:\Users\Calvin\Pictures\Saved Pictures\8、java面对对象三大特性.png)

