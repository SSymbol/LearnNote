## 数组
### 动态初始化：
指定长度 int[] array1= new int[20]
可拆分为两个步骤 int[] array1; array1 = new int[20];
默认值 整型为0 浮点型0.0 字符类型'\u0000' （\u表示unicode 0000十六进制字符类型默认值）
布尔型默认false  引用类型默认null

### 静态初始化：
指定内容 int[] array2= new int[] {1, 12, 23, 34, 55, 66};
string array3 = new int[]  {"hello", "world", "java"};
静态初始化同样有长度
*注意* 内存中静态初始化过程中元素先为默认值 后赋值大括号内的初始值
可拆分为两个步骤： int[] array2; array2= new int[] {1, 12, 23, 34, 55, 66};


### 省略格式的静态初始化：
int[] array4= {1, 2, 3, 4, 5};
省略格式*不能*拆分,例如:
```
int[] array4; array={1, 2, 3, 4, 5};
```
### 元素获取
System.out.println(array1);//直接打印数组名称 -> 数组对应的内存地址哈希值 
[I@75412c2f [表示数组 I表示int型 @后面是16进制
System.out.println(array1[0]);
int num = System.out.println(array1[1]);
array1.length 数组长度 且不可改变


ArrayIndexOutofBoundsException数组索引越界异常 ：int num = System.out.println(array1[3]); 溢出
定义了数组但不初始化，即时只赋值null，并不进行new创建，则发生空指针异常，NullPointerException



