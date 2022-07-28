今日内容:

1. 循环结构的语句

   for, while,  do  while

2. Random类

   功能: 获取随机数

3. 综合案例

# 一. 循环结构语句

## 1.1  循环结构语句概述

概述: 循环语句指的重复执行代码.

特点:

1. 代码重复执行
2. 循环有开始, 有结束, 如果没有结束的循环,称之为死循环

图示一: 

![11](imgs/s1.png)

图示二:

![111](imgs/s11.png)



## 1.2 for循环介绍

* 语法格式:

  ~~~~java
  初始化语句: 指的循环的起始位置(比如: 图示二,小动物的起跑位置)
  条件判断语句:通过条件判断语句,来确定循环是否继续(比如:图示二,当小动物跑完10000米,循环结束了)
  条件控制语句: 通过条件控制语句来控制循环执行的次数(或者说循环是否结束)(比如: 图示二,当小动物跑完25圈)
  循环体语句: 指的循环重复执行的代码    
  for(初始化语句;条件判断语句;条件控制语句){
      
      循环体语句;
      
  }
  ~~~~

* 执行流程, 如图

  ![111](imgs/s2.png)



执行步骤:

1. 执行初始化语句

2. 进行条件判断语句

   如果条件判断的结果为false, 循环体语句就不执行了

   如果条件判断的结果为true,执行循环体语句

3. 执行完循环体语句以后,然后再执行条件控制语句

   重复第2步

4. 循环结束以后,执行其他语句

## 1.3 for循环入门案例

* 需求: 打印10次1.

分析:

10次1 :  重复执行的语句

~~~~java
/**
 * 演示: for完成打印10次1
 */
public class Demo1 {
    public static void main(String[] args) {
        /**
         * i=0: 指的循环的起始位置
         * i<=9: 指的循环条件判断语句
         * i++ : 指的循环控制条件, 每次对i=i+1
         * 循环体语句: System.out.println("重复的语句:"+1);
         */
        
        for(int i=0;i<=9;i++){
            System.out.println("重复的语句:"+1);
        }
        for(int i=1;i<=10;i++){
            System.out.println("重复的语句:"+1);
        }
    }
}
~~~~

* 需求: 

  打印1,2,3,4,5

  需求:

  打印 5,4,3,21

~~~~java
public class Demo2 {
    public static void main(String[] args) {
        //打印1, 2,3,4,5
        for (int i = 1; i <=5 ; i++) {
            System.out.println(i);
        }
        System.out.println("-------------------------");
        //打印5,4,3,2,1
        for (int i = 5; i >0 ; i--) {
            System.out.println(i);
        }
    }
}
~~~~

* 上楼梯案例:

~~~~java
public class Demo2 {
    public static void main(String[] args) {
        //需求: 上楼梯, 一次上一个台阶,楼梯一共10个台阶
        for (int i = 1; i <=10 ; i++) {
            System.out.println("上台阶:"+i);
        }
        System.out.println("-------------------------");
       //需求: 上楼梯, 一次上二个台阶,楼梯一共10个台阶
        for (int i = 0; i <=10 ; i+=2) {
            System.out.println("上台阶:"+i);
        }
    }
}

~~~~



* 小动物运动会案例

  需求一:  打印小动物的跑的圈数

  需求二: 打印小动物跑的圈数, 以及跑了多少米

  ~~~~java
  /**
   * 小动物运动会案例
       需求一:  打印小动物的跑的圈数
       需求二: 打印小动物跑的圈数, 以及跑了多少米
   */
  public class Demo1 {
      public static void main(String[] args) {
          //需求二: 打印小动物跑的圈数, 以及跑了多少米
          /**
           * i=0; 说明小动物起跑位置0
           * i<=10000;条件判断, 说明小动物抛到10000米,就不跑了
           * i+=400; 条件控制语句, 说明小动物每圈跑400
           */
          //定义一个变量,来表示跑的第几圈
          int count=0;//第0圈
          for (int i = 0; i <=10000 ; i+=400) {
              System.out.println("跑的是第"+count+"圈,跑的"+i+"米");
              //每跑一圈,对count=count+1
              count++;
          }
  
      }
  
      private static void test1() {
          //跑10000米, 每圈400米,打印小动物的跑的圈数
          /**
           * i=0 ;起始位置, 说明小动物还没有起跑
           * i<=25; 条件判断, 一共25
           * i++: 条件控制
           */
          for (int i = 0; i <=10000/400 ; i++) {
              System.out.println("跑的第"+i+"圈");
          }
      }
  }
  
  ~~~~

## 1.4 while循环

* 语法格式

  ~~~~java
  初始化语句;
  while(条件判断语句){
      循环体语句;
      条件控制语句;
      
  }
  ~~~~

  

* 执行流程,如图

  ![111](imgs/s2.png)



   执行顺序(步骤):

1. 执行初始化语句(指的循环起始位置)

2. 执行条件判断语句

   如果条件判断结果为false, 结束循环

   如果条件判断结果为true,执行循环体

3. 执行每句循环体语句以后,再执行条件控制语句

   重复第2步执行

4. 循环结束,执行其他语句.

* while循环打印1-10 或者 10-1

  ~~~~java
  /**
   * while循环打印1-10 或者 10-1
   */
  public class Demo3 {
      public static void main(String[] args) {
          //打印10--1
          //1.定义初始化语句
          int endLocation = 10;
          //2.while
          while(endLocation>0){//条件判断语句
              System.out.println(endLocation);//循环体
              endLocation--;//条件控制语句
          }
  
      }
  
      private static void test1() {
          //打印: 1-10;
          //1.定义初始化语句,变量
          int beginLocation=1;//循环的起始位置
          //2.while
          while(beginLocation<=10){//条件判断语句
              System.out.println(beginLocation);//循环体
              beginLocation++;//条件控制语句
          }
      }
  }
  
  ~~~~

  

* while改造上面的for循环案例

  ~~~~java
public class Demo2 {
    public static void main(String[] args) {
        /**
         * 需求上楼梯,每次上2个台阶,一共10个台阶
         */
        //1.定义初始化语句
        int step=0;
        //2.while循环
        while (step<=10){//条件判断语句: step<=10
            System.out.println("上第"+step+"个台阶");//循环体语句
            step+=2;//条件控制语句
        }

    }

    private static void test1() {
        /**
         * 需求上楼梯,每次上一个台阶,一共10个台阶
         */
        //1.定义初始化语句
        int step=1;
        //2.while循环
        while (step<=10){//条件判断语句: step<=10
            System.out.println("上第"+step+"个台阶");//循环体语句
            step++;//条件控制语句
        }
    }
}
  ~~~~



## 1.5 while和for循环区别

* while和for循环相同点

  执行流程是一样的.

* while和for循环区别

  1. for循环初始化语句对应的变量, 循环结束以后,就不能使用了

     如图:

     ![image-20220704103352849](imgs/image-20220704103352849.png)

  2. while循环初始化语句对应的变量, 循环结束以后,可以继续使用

     ![image-20220704103542210](imgs/image-20220704103542210.png)

  3. for循环,必须清楚循环的起始位置,也就是说必须定义初始化语句.

  4. while循环, 可以不清楚循环的起始位置,也就是说不用定义初始化语句.

  5. 案例: 折纸案例

     需求:  纸张厚度是0.1毫米, 当纸折多少次,能超出珠穆朗玛峰的高度.

     ~~~~java
     /**
      *  案例: 折纸案例
         需求:  纸张厚度是0.1毫米, 当纸折多少次,能超出珠穆朗玛峰的高度.
         分析:
             循环折纸, 不清楚循环的起始位置.
      */
     public class Demo5 {
         public static void main(String[] args) {
             //1.定义纸张的厚度
             double paper = 0.1D;//0.2,0.4,0.8
             //2.定义珠穆朗玛峰的高度:固定的,使用常量表示
             final double Z_H=8844330.0;
             //定义一个变量,表示折纸的次数
             int count=0;
             //3.while循环
             while(paper<=Z_H){//条件判断语句
                 paper*=2;//循环体语句
                 count++;//每次X2,表示折纸一次
             }
             System.out.println("折纸次数: "+count+",折纸的高度:"+paper);
         }
     }
     
     ~~~~

     

## 1.6 死循环

* 死循环概述

  指的循环体语句一直执行,不会停下来.

  死循环造成的问题:  内存溢出(指的内存空间不够用了,电脑会死机 )

* 死循环的语法

  * 方式一:

    ~~~~java
    for(;;){
        循环体语句;//会一直执行,不会停
    }
    ~~~~

  * 方式二:

    ~~~~java
    while(true){
         循环体语句;//会一直执行,不会停
    }
    ~~~~

    

## 1.7 do--while循环

* 语法格式

  ~~~~~java
  初始化语句
  do{
      循环体语句; 
      条件控制语句;
  }while(条件判断语句);
  ~~~~~

* 执行流程, 如图

  ![11](imgs/s3.png)



执行流程:

1. 执行初始化语句

2. 执行循环体语句

3. 执行条件控制语句,然后在执行条件判断语句

   条件判断的结果为false, 结束循环

   条件判断的结果为true, 重复从第2步开始执行

4. 循环结束,执行其他语句.

* do- while循环改造上面的案例

  1. 打印1-10或者10-1

  2. 打印1-10或者10-1之间的偶数

  3. 打印1-10或者10-1之间的奇数

     ~~~~java
     public class Demo1 {
         public static void main(String[] args) {
             //打印10-0的奇数
             //1.定义初始化语句
             int begin=10;
             //2.do while
             do{
               if(begin%2!=0){//奇数的判断条件
                   System.out.println(begin);
               }
                 begin--;//循环控制
             }while (begin>=0);//条件判断
     
     
         }
     
         private static void test3() {
             //打印10-0的偶数
             //1.定义初始化语句
             int begin=10;
             //2.do while
             do{
                 System.out.println(begin);//循环体
                 begin-=2;//循环控制
             }while (begin>=0);//条件判断
         }
     
         private static void test2() {
             //1.定义初始化语句
             int begin=10;
             //2.do--while
             do{
                 System.out.println(begin);//循环体
                 begin--;//循环控制语句
             }while(begin>0);//条件判断语句
         }
     
         private static void test1() {
             //打印 1-10
             //1.定义初始化语句
             int i=1;
             do{
                 System.out.println(i);//循环体语句
                 i++;//循环控制语句,控制循环执行的次数
             }while (i<=10);
         }
     }
     
     ~~~~

     

## 1.8 do-while 和while(for)的区别

* do---while

​       由于do-while先执行循环体语句, 所以不管条件判断是否满足, do-while至少执行一次循环体语句.

* while(for)

  由于先执行条件判断语句,然后再执行循环体语句, 所以while再执行时,如果条件不满足,不会执行循环体语句.

* 代码演示

  ~~~~java
  public class Demo2 {
      public static void main(String[] args) {
          // do - while
          int i=1;
          do{
              System.out.println(i);//条件不成立,一会打印i=1
              i++;
          }while (i<-2);//条件不成立
          // while
          int sum=100;
          while(sum<=0){//条件不成立
              System.out.println(sum);//不执行循环体语句
              sum--;
          }
      }
  }
  ~~~~

## 1.9 break和continue

* break

  1. switch分支语句中, 使用break,用来结束分支语句的执行
  2. 循环语句,使用break,用来结束循环(跳出循环)

* continue

    只能应用与循环语句中, 用来结束本次循环(终止某个循环体语句的执行),可以继续下次循环(继续执行下个循环体语句).

* 案例

  案例一: 打印1-10之间的数字,其中5不打印

  案例二: 打印1-10之间的数字, 遇到了5,后面不在打印

  ~~~~~java
  public class Demo1 {
      public static void main(String[] args) {
          //案例二: 打印1-10,遇到了5 ,后面的数字不在打印
          for (int i = 1; i <=10 ; i++) {
              System.out.println(i);
              //其中5不打印
              if(i==5){
                  break;//5这个循环体不执行,其它循环语句不执行, 循环结束
              }
  
          }
      }
  
      private static void test1() {
          //案例一: 打印1-10之间的数字,其中5不打印
          for (int i = 1; i <=10 ; i++) {
              //其中5不打印
              if(i==5){
                  continue;//5这个循环体不执行,其它循环语句继续执行
              }
              System.out.println(i);
          }
      }
  }
  
  ~~~~~

# 二.综合案例

## 案例一: 求和

1.计算 1 + 2 + 3 + 4 + 5 ... + 98 + 99 + 100 的总和。

思路:

1. 遍历从1到100

2. 定义变量来接收和

   ~~~~java
   public class Demo2 {
       public static void main(String[] args) {
           /**
            * 1.计算 1 + 2 + 3 + 4 + 5 ... + 98 + 99 + 100 的总和。
            思路:
            1. 遍历从1到100
            2. 定义变量来接收和
            */
           //1.定义变量
           int sum=0;
           //2. 遍历1-100
           for (int i = 1; i <=100 ; i++) {
               //3.求和
               sum+=i;
           }
           //4.打印
           System.out.println(sum);
   
   
       }
   }
   
   ~~~~

## 案例二: 1-100之间的偶数的 和

~~~~~java
public class Demo2 {
    public static void main(String[] args) {
        /**
         * 1.计算 1 + 2 + 3 + 4 + 5 ... + 98 + 99 + 100 的总和。
         思路:
         1. 遍历从1到100
         2. 定义变量来接收和
         */
        //1.定义变量
        int sum=0;
        //2. 遍历1-100
        for (int i = 1; i <=100 ; i++) {
            //3.判断数字是否是偶数
            if(i%2==0){//i是偶数
                //4.求和
                sum+=i;
            }
        }
        //4.打印
        System.out.println(sum);


    }
}
~~~~~



## 案例三:  计算10的阶乘。

~~~~java
public class Demo3 {
    public static void main(String[] args) {
        //1.定义一个变量,来接收乘积
        int multi=1;
        //2.遍历1-10
        for (int i = 1; i <=10 ; i++) {
            //3.乘积
            //第一次循环: multi=multi*1=1
            //第二次循环: multi = multi*2=2
            //第三次循环: multi = multi*3=6
            //---
            multi*=i;
        }
        //4.打印结果
        System.out.println(multi);
    }
}
~~~~



## 案例四:打印闰年

打印1500-2021之间的闰年
能被4整除，不能被100整除的年。
能被400整除的年。

## 案例五: 打印猪年

需求: 获取1949-2019年之间的猪年, 其中2019是猪年.

思路:

1. 遍历从1949---2019
2. 判断猪年:  (2019-遍历的年份数据)%12==0 就是猪年.

~~~~java
/**
 * '需求: 获取1949-2019年之间的猪年, 其中2019是猪年.
 思路:

 1. 遍历从1949---2019
 2. 判断猪年:  (2019-遍历的年份数据)%12==0 就是猪年.
 */
public class Demo4 {
    public static void main(String[] args) {
        //1.遍历年份
        for (int i = 1949; i <=2019 ; i++) {
            //2.判断
            if((2019-i)%12==0){
                System.out.println("猪年是:"+i);
            }
        }
    }
}
~~~~



**案例六: 跑步,中途放弃**
小张参加长跑比赛5000米，一共10圈，如果小张坚持不下来，抛到第6圈中途退出比赛，使用程序描述这个场景?

## 案例七: 跑步,中途可以喝水,但是必须坚持下去

要求：小张参加长跑比赛5000米，一共10圈，如果小张口渴了，喝水后继续跑，使用程序描述这个场景?

~~~~java
public class Demo5 {
    public static void main(String[] args) {
        //小张参加长跑比赛5000米，一共10圈，如果小张坚持不下来，
        // 抛到第6圈中途喝水,继续比赛，使用程序描述这个场景
        //1.定义一个变量,来接收小张跑的圈数
        int count=0;
        for (int i = 0; i <=5000 ; i+=500) {
            System.out.println("跑的"+(count++)+"跑的"+i+"米");
            if(count==6){
                System.out.println("中途喝水");
                continue;
            }
          
        }

    }

    private static void test1() {
        //小张参加长跑比赛5000米，一共10圈，如果小张坚持不下来，
        // 抛到第6圈中途退出比赛，使用程序描述这个场景
        //1.定义一个变量,来接收小张跑的圈数
        int count=0;
        for (int i = 0; i <=5000 ; i+=500) {
            System.out.println("跑的"+(count++)+"跑的"+i+"米");
            if(count==6){
                break;
            }
        }
    }
}
~~~~



# 三.Random类

## **1.1 Random类**概述

作用:  Random这个类的作用就是获取随机数

## 1.2 常用方法

- `nextInt()`:   获取一个任意的随机数
- `nextInt(int bound)`: 获取一个[0, bound)的随机数(获取一个大于等于0, 并且小于 bound的随机数)

## 1.3 入门程序

* 步骤一:  导入包名

  ~~~~java
  import java.util.Random;
  ~~~~

  

* 步骤二:  创建随机数对象

  ~~~~~java
     //2.步骤二:  创建随机数对象
      Random rd = new Random();
  ~~~~~

  

* 步骤三: 通过对象调用方法

* ~~~~~java
  public class Demo1 {
      public static void main(String[] args) {
          /**
           * 步骤一:  导入包名
           * 步骤二:  创建随机数对象
           * 步骤三: 通过对象调用方法
           */
          //2.步骤二:  创建随机数对象
          Random rd = new Random();
          //3.步骤三: 调用方法
          for (int i = 0; i <100 ; i++) {
              //int randNumber = rd.nextInt();
              int randNumber = rd.nextInt(10)+1;//[1,10]
              System.out.println(randNumber);
          }
      }
  }
  
  ~~~~~

# 四. 案例之猜数字游戏

  需求:

​     系统生成一个随机数的范围1-100, 用户通过键盘录入一个数字,与系统生成的随机数字进行比较.

 思路:

1. Random生成一个1-100之间的随机数
2. Scanner录入一个数字
3. 死循环,猜不对数字一直猜, 当猜对数字使用break.

~~~~java
/**
 需求:
 系统生成一个随机数的范围1-100, 用户通过键盘录入一个数字,与系统生成的随机数字进行比较.
 思路:
 1. Random生成一个1-100之间的随机数
 2. Scanner录入一个数字
 3. 死循环,猜不对数字一直猜, 当猜对数字使用break
 */
public class Demo2 {
    public static void main(String[] args) {
        //1.创建一个Random对象
        Random rd = new Random();
        //2.获取一个随机数: 1-100
        int randNumber =  rd.nextInt(100)+1;
        //3.创建一个键盘录入对象
        Scanner sc = new Scanner(System.in);
        //4.死循环
        while (true){
            //5.获取用户录入的数字
            System.out.println("请录入数字:");
            int recodeNumber = sc.nextInt();
            //5.在循环里面判断 数字是否猜对, 猜对数字了使用break结束
            if(recodeNumber>randNumber){//大于系统生成的数字
                System.out.println("输入的数字:"+recodeNumber+"大了");
            }else if(recodeNumber<randNumber){//小于系统生成的数字
                System.out.println("输入的数字:"+recodeNumber+"小了");
            }else{//等于系统生成的数字, 猜对,循环结束
                System.out.println("恭喜你,猜对了");
                break;//猜对了,跳出循环
            }
        }

    }
}

~~~~



# 五. 嵌套循环

* 嵌套循环概述

   循环中嵌入了循环,这种写法就是嵌套循环.

  语法格式:

  ~~~~java
  // 嵌套了两层循环
  for(----){//外层循环
      for(----){//内层循环
          
      }
      
  }
  // 嵌套了两层循环
  for(----){//外层循环
      while(----){//内层循环
          
      }
      
  }
  // 嵌套了两层循环
  for(----){//外层循环
      do{//内层循环
          
      }while(--);
      
  }
  // 嵌套了两层循环
  while(----){//外层循环
      for(---){//内层循环
          
      }
      
  }
  ~~~~

  两层嵌套循环的执行流程:

  1. 执行外层循环的初始化语句

  2. 执行外层循环的 条件判断语句

     如果外层循环的条件判断的结果是false, 整个循环结束了

     如果外层循环的条件判断结果是true, 那么执行内层循环(内层循环的执行流程和单个for或者单个while或者单个do while)一样

  3. 如果内层循环执行完毕以后, 接着执行外层循环的条件控制语句.

     重复从第2步的执行

  4. 循环结束,执行其他语句.

  

  **案例一:**

   需求:  打印3个班的前5名学生的学号. 班级编号: 001, 002, 003, 学号1,2,3,4,5数字来表示.

  ~~~~~java
  /**
   * 案例一:
      需求:  打印3个班的前5名学生的学号. 班级编号: 001, 002, 003, 学号1,2,3,4,5数字来表示.
      思路:
        循环: 可以遍历班级, 学号也需要遍历
   */
  public class Demo1 {
      public static void main(String[] args) {
          //1.在外层 : 遍历循环班级
          for (int i = 1; i <=3 ; i++) {
              System.out.print("00"+i+"班级: ");//打印班级
              //2.在内层循环里面: 遍历学生的学号
              for (int j = 1; j <=5 ; j++) {
                  System.out.print(j+"号"+",");
              }
              System.out.println();//每打印一个班级,换一行
          }
      }
  }
  ~~~~~

  **案例二:  打印5*5正方形**

  ~~~~~java
  /**
   * 案例二: 用*表示, 打印5*5的正方形
   * 分析:
   *   行: 外层循环
   *   列: 内层循环
   */
  public class Demo2 {
      public static void main(String[] args) {
          //1.定义行
          int  row = 5;
          //2.定义列
          int column = 5;
          //3.嵌套循环
          //4.循环行
          for (int i = 1; i <=row ; i++) {
              //System.out.print(i);
              //5.内层循环: 循环列, 打印一行的5个*
              for (int j = 1; j <=column ; j++) {
                  System.out.print("*");
              }
              //6.打印完一行* 以后, 换行
              System.out.println();
          }
      }
  }
  ~~~~~

  **案例三:  打印5行的直角三角形**

  ~~~~~java
  /**
   * 案例: 打印5行的直角三角形, 用*表示
   *  外层循环: 打印行数1-5
   *  内层循环: 打印列数(*个数), *的个数<=行数
   */
  public class Demo3 {
      public static void main(String[] args) {
          //1.定义行数
          int row = 5;
          //2.列数(其实*的个数)小于等于行数
          int startCount=1;
          //3.外层循环
          for (int i = 1; i <=row ; i++) {
              //内层循环, 打印每行*的个数
              for (startCount = 1; startCount <=i ; startCount++) {
                  System.out.print("*");
              }
              //每行打印完毕,换行
              System.out.println();
          }
      }
  
  }
  ~~~~~

  **案例四: 打印9*9乘法表**

  ![image-20220704163452058](imgs/image-20220704163452058.png)

  ~~~~~java
  /**
   * 案例四: 9*9
   */
  public class Demo4 {
      public static void main(String[] args) {
          //思路: 打印直角三角形一样
          //1.定义行数
          int row = 9;
          //2.定义列数
          int column=1;
          //3.嵌套循环
          //4.外层循环: 行数 9
          for (int i = 1; i <=9 ; i++) {
              //5.内层循环: 循环列数 , 小于等于行数i. 比如: 1行: 1*1 ,2行: 1*2, 2*2
              for (column=1; column <=i ; column++) {
                  // \t 制表符号, 让表格看起来好看一点
                  // 拼接:1*1=(1*1)
                  System.out.print(i+"*"+column+"="+(i*column)+"\t");
              }
              System.out.println();
          }
      }
  }
  ~~~~~

  

  **案例五: 打印直角梯形**

  

  **案例六: 打印等腰三角形**
