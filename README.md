# 创建Android项目（基于Cordova 6.4.0）  
1. 创建项目 
在命令窗口打开项目根目录（执行cd 目录名），执行cordova create  子项目名    package包名   应用名   
(例如 `cordova   create  hello com.example.hello  helloWorld`)  

2. 添加平台  
到项目目录，检查支持平台`cordova platforms ls`  
在命令窗口打开项目目录（例如 cd hello），执行`cordova platform add android`  

3. 构建应用  
在命令窗口执行`cordova build android`  

4. 手机测试  
在命令窗口执行`cordova run android`  

5. 安装调试工具  
Corova Tools目前的主要功能是更方便的开发调试  
* Run Android on device ：真机测试  
* Run Android on simulator：模拟器测试  
* Simulate Android in browser：在浏览器中测试

6. 目录介绍
* config.xml：Cordova的核心配置信息   
* hook ：自定义扩展功能  
* platform ：支持的平台，例如Andriod、iOS等  
* plugins ：插件目录  
* www ：web目录  

7. 插件  
cordova plugin add <插件官方名称>  
cordova plugin rm <插件官方名称>  



# 解析Java注解  
1. 注解概念  
注解概念:java提供了一种源程序中的元素关联任何信息和任何元数据的一种途径和方法  

2. java常见注解  
* @Override：重写父类的该函数，编译器可以给你验证@Override下面的方法名是否是你父类中所有的,如果没有则报错，比如你如果没写@Override而你下面的方法名又写错了,这时你的编译器是可以通过的(它以为这个方法是你的子类中自己增加的方法)  
* @Deprecated: 表示该函数已过时    
* @SuppressWarning:忽略某某警告  
前两个都是用在父类，下面用在子类  

3. 常见第三方注解  
Spring: 	@Autowired      @Service    @Repository  
* @Autowired: 可以对成员变量、方法和构造函数进行标注，来完成自动装配的工作  
* @Service：定义某个类为一个bean，则在这个类的类名前一行使用@Service("XXX"),就相当于讲这个类定义为一个bean，bean名称为XXX。而无需去xml文件内去配置  
* @Repository：用于标注数据访问组件，即DAO组件  

4. 自定义注解
自定义注解语法要求  
* 用关键字@interface定义注解， 如：public @interface AnnotationDemo { }  
* 成员以无参无异常的方式声明，可以用default为成员指定的一个默认值  
* 成员类型是受限的，只能是原始类型及String, Class, Annotation, Enumeration  
* 如果注解只有一个成员，则成员名必须为value()，在使用时可以忽略成员名和赋值号（=）  
* 标识注解：没有成员的注解  
* 元注解：   

        @Target：注解的作用域（使用枚举类型ElementType的成员进行标识，可同时指定多个）  
        § ElementType包括：TYPE(类或接口),  FIELD(字段),  METHOD,  PARAMETER,  CONSTRUCTOR,  LOCAL_VARIABLE,  ANNOTATION_TYPE,  PACKAGE,  TYPE_PARAMETER,  TYPE_USE  

        @Retention：生命周期（使用枚举类型RetentionPolicy的成员进行标识）  
        § RetentionPolicy包括：SOURCE,  CLASS,  RUNTIME 

        @Inherited：允许子注解继承  

        @Documented：生成javadoc文档时会包含注解  

```java
@Target({ElmentType.METHOD,ElementType.Type})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
public @ interface Description{
	String desc();
	String author();
	int age() default18;
}
```  

5. 注解应用实战
* 使用注解的语法  
```java
@<注解名>(<成员名1>=<成员值1>,<成员名2>=<成员值2>,...)
@Description(desc ="I am eyeColor",author="C boy",age=18)
public String eyeColor(){
	return "red";
}
```  

* 解析注解  
    * 使用类加载器加载类（Class.forName）  

    * 获取类上的注解（可以先判断注解是否存在）  
        ```java 
        public boolean isAnnotationPresent(Class<? extends Annotation> paramClass)
        ```  

    * 拿到注解实例  
        ```java 
        public <A extends Annotation> A getAnnotation(Class<A> paramClass)
        ```   
        使用实例获取成员的值（如d.value()）  

    * 获取方法上的注解  
        通过反射拿到类上的所有方法，返回Method数组  
            § public Method[] getMethods()
        遍历Method数组取得方法上的注解（可以先判断注解是否存在）  
            § public boolean isAnnotationPresent(Class<? extends Annotation> paramClass)  
        拿到方法上注解的实例  
            § public <A extends Annotation> A getAnnotation(Class<A> paramClass)  
        使用实例获取成员的值（如d.value()）  

    * 获取方法上注解也可以使用getAnnotations获取Method数组中的全部注解  
        ```java
        public Annotation[] getAnnotations()  
        ```  



# 遇到的坑  
1. 添加平台时，如果有中文路径，`cordova-plugin-whitelist`会报错  


# 参考文献  
* [Android 教程](https://www.w3cschool.cn/android/android-tutorial.html)
* [Apache Cordova开发环境搭建](https://blog.csdn.net/u011127019/article/details/56335719)  
* [VS Code插件之Cordova Tools](https://blog.csdn.net/u011127019/article/details/59137579)  
* [全面解析Java注解](https://blog.csdn.net/mqy1023/article/details/50565057)  
* [注解反射生成SQL语句](https://blog.csdn.net/zen99t/article/details/50351575)