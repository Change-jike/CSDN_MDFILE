> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/123264100?spm=1001.2014.3001.5502)

### [数组](https://so.csdn.net/so/search?q=%E6%95%B0%E7%BB%84&spm=1001.2101.3001.7020)操作与实际案例分析

数组是一个连续的数据存储空间，同时带有下标性质的操作，下标范围是 0 ~ 数组容量 - 1.

**数组的数据操作需要执行下标合法性判定！！！**  
执行下标子在合法范围以内，如果超出合法范围，提示用户操作错误！！！

##### 1. 数组和 for 循环不得不说的事儿

```
/* 
1. 利用 for 循环给予数组中的每一个元素进行赋值操作
2. 利用 for 循环展示数组中的每一个元素数据存储内容
*/ 
class Demo1 {
	public static void main(String[] args) {
		// 1. 定义一个 int 类型数组
		int[] arr = new int[10];
		
		/*
		2. 利用 for 循环进行赋值操作
		数组下标从 0 开始，到数组容量 - 1，步进关系为 1 
		*/
		for (int i = 0; i < arr.length; i++) {
			arr[i] = i * 2;
		}
		
		/*
		3. 利用 for 循环展示数组中存储的数据内容
		*/
		for (int i = 0; i < arr.length; i++) {
			System.out.println(arr[i]);
		}
	}
}

```

##### 2. 找出数组中指定元素第一次出现的下标位置

**分析：**

```
	1. 在目标数组中找出对应元素下标位置，找到后返回对应下标，没找到返回 -1 。
	2. 在数组中，元素的下标范围是 ==> 0 ~ 数组容量 - 1【0 ~ 数组容量 - 1 是**合法下标**范围】，所以 -1 一定是一个非法下标。
	3. 数组中有多个相同元素存在，找到第一个目标的位置，即刻终止循环！！！利用 **break** 关键字跳出循环。
	4. **break** 关键字有且只可以跳出一层循环结构

```

```
/*
2. 找出数组中指定元素第一次出现的下标位置
*/
class Demo2 {
	public static void main(String[] args) {
		/*
		1. 定义一个 int 类型数组，并且进行数据赋值操作
		静态数组创建方式
			a. 数组容量由大括号中有多少个元素决定
			b. 数组数据存储情况根据当前大括号中数据元素内容决定
		*/
		int[] arr = {1, 3, 5, 7, 9, 1, 3, 5, 7, 9};
		// 目标查询元素
		int num = 5;
		
		/*
		2. 定义一个变量存储目标数据下标位置
			a. 后期需要利用 for 循环遍历数组，同时 if 判断找出对应元素下标位置
			b. 如果 if 判断结果为 true， index 重新被赋值，赋值内容就是目标下标位置
			c. 如果 if 判断结果始终为 false, 目标元素不存在，index值还是 -1 可以用于提示
			后续使用者，目标元素在当前数组中不存在，
		*/
		int index = -1;
		
		/*
		3. 利用 for 循环遍历整个数组，if 判断找出目标元素下标位置
		*/
		for (int i = 0; i < arr.length; i++) {
			// 判断数组中下标为 i 的元素是否和用户指定数据 num 一致
			if (num == arr[i]) {
				// index 保存当前下标内容
				index = i;
				// 利用 break 关键字跳出循环结构
				break;
			}
		}
		
		// 4. 判断 index 数据情况，得到目标是否存在，和存在对应下标位置
		if (index > -1) {
			System.out.println("目标元素所在下标位置:" + index);
		} else {
			System.out.println("Source Not Found!!!(未找到)");
		}
	}
}

```

**注意：** 找出数组中指定元素最后一个出现的下标位置时，整体代码流程和找出数组中指定元素第一次出现下标位置一致，但是需要从数组的最后一个下标位置向前找出对应元素。

1.  for 循环从最后一个有效元素下标位置开始，倒置循环，到下标为 0 终止，步进关系为 i–。
2.  循环终止条件为 i >= 0 ; 0 也是数组的有效下标

##### 3. 数组元素的逆序

**要求:**

​ 原数组:  
​ int[] arr = {1, 3, 5, 7, 9, 2, 4, 6, 8, 10};  
​ 逆序之后:  
​ arr ===> {10, 8, 6, 4, 2, 9, 7, 5, 3, 1};

**分析：**

1.  数据的前后交换次数 = 数据容量 / 2
2.  循环从下标为 0 的位置开始

```
// 数组元素逆序
class Demo4 {
	public static void main(String[] args) {
		// 1. 源数据数组
		int[] arr = {1, 3, 5, 7, 9, 2, 4, 6, 8};
		
		// 2. 利用 for 循环逆序数组内容
		for (int i = 0; i < arr.length / 2; i++) {
			int temp = arr[i];
			arr[i] = arr[arr.length - 1 - i];
			arr[arr.length - 1 - i] = temp;
		}
		
		// 3. 展示数据存储结果
		for (int i = 0; i < arr.length; i++) {
			System.out.println(arr[i]);
		}
	}
}

```

##### 4. 复制数组数据到新数组

**要求：**

源数据数组  
int[] arr = {1, 3, 5, 7, 9, 2, 4, 6, 8, 10}；  
复制数组中 下标 3 到 下标 6 之间的数据到新数组  
新数组数据容量和内容如下  
int[] newArr = {7, 9, 2}；

**分析：**

1.  从数组中复制数据到型数组内，采用条件是要头不要尾，左闭右开区间，[3 ， 6) ==> 要下标 3 下的内容 ， 不要下标 6 下的数据内容。
2.  **计数器：**

初始化为 0 的一个临时变量，每进行一次复制数据，累加 1 。

**作用：**

1.  记录当前数组有多少个有效元素。
2.  作为下一次存放元素的下标位置

![](https://i-blog.csdnimg.cn/blog_migrate/5d7d27dc9f12bae8a69ead5d9bc36b61.png)

```
// 复制数组数据到新数组
class Demo5 {
	public static void main(String[] args) {
		// 1. 源数据数组
		int[] arr = {1, 3, 5, 7, 9, 2, 4, 6, 8, 10};
		// 2. 起始下标
		int begin = 3;
		int end = 6;
		
		// 3. 计算得到新数组容量
		int newCapacity = end - begin;
		
		// 4. 根据新数组容量创建 int 类型数组存储指定截取数据
		int[] newArr = new int[newCapacity];
		
		// 5. 定义计数器
		int count = 0;
		
		// 6. 按照指定范围要求复制数据到新数组中
		for (int i = begin; i < end; i++) {
			newArr[count] = arr[i];
			count += 1;
		}
		
		// 7. 展示新数组数据结果
		for (int i = 0; i < newArr.length; i++) {
			System.out.println(newArr[i]);
		}
	}
}

```

##### 5. 找出数组中最大值的下标位置

**分析：**

1.  首先假设下标为 0 的元素为最大值，使用 int 类型变量保存
2.  循环从小标为 1 的元素开始，到整个元素的最后一个元素，两两比较。

```
// 找出数组中的最大值下标位置
class Demo6 {
	public static void main(String[] args) {
		// 1. 源数据数组
		int[] arr = {100, 3, 5, 7, 19, 2, 4, 6, 8, 20};
		
		// 2. 假设下标为 0 的元素为最大值，使用 int 类型变量 maxIndex 保存
		int maxIndex = 0;
		
		// 3. for 循环从下标为 1 的元素开始，到整个数组的最后一个元素，进行两两比较，最大值下标
		// 存储到 maxIndex 中
		for (int i = 1; i < arr.length; i++) {
			// 4. 如果 maxIndex 下标对应元素，小于下标为 i 的元素，maxIndex 存储下标 i
			if (arr[maxIndex] < arr[i]) {
				maxIndex = i;
			}
		}
		
		// 4. 展示最大值下标数据情况
		System.out.println("最大值下标位置:" + maxIndex);
	}
}

```

##### 6. 在数组指定下标位置添加元素

**要求：**

​ 添加指定元素 20 到下标为 5 的位置  
​ {1, 3, 5, 7, 9, 20, 11, 13, 15, 17};

**注意：**

1.  0 为无效元素，仅占位使用
2.  插入数据下标的位置必须在合法范围以内

![](https://i-blog.csdnimg.cn/blog_migrate/dd5eeb18f55b52f91378b8ae595ef157.png)

```
// 在数组指定下标位置添加元素
class Demo9 {
	public static void main(String[] args) {
		// 1. 准备源数据数组，指定下标位置 index，和目标添加元素 num
		int[] arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 0};
		int index = 0;
		int num = 20;
		
		// 2. 判断用户指定的下标位置是否为 合法下标
		if (index > arr.length - 1 || index < 0) {
			// 提示用户操作失败
			System.out.println("您输入的下标不合法！！！");
			// 终止程序运行
			System.exit(0);
		}
		
		/*
		3. for 循环完成，循环从最后一个【有效元素】下标位置开始，到用户
		指定添加元素下标结束。
		*/
		for (int i = arr.length - 1; i > index; i--) {
			arr[i] = arr[i - 1];
			/*
			arr[9] = arr[8];
			arr[8] = arr[7];
			arr[7] = arr[6];
			arr[6] = arr[5];
			*/
		}
		
		// 4. 将元素放入指定下标位置
		arr[index] = num;
		
		/*
		5. 利用 for 循环展示数组中存储的数据内容
		*/
		for (int i = 0; i < arr.length; i++) {
			System.out.println(arr[i]);
		}
	}
}

```

**删除数组中指定下标元素内容时**

** 注意：** 用户删除数组中元素，如果用户未持有被删除元素本身，建议在删除操作过程中，对被删除的元素内容进行一定程度的保护。

##### 7. 找出数组中指定元素的所有对应下标位置

**要求：**

1.  目标数据下标位置存储到另一个数组中  
    例如：
    
    ​ 目标数组：
    
    int[] arr = {1, 3, 5, 1, 3, 5, 1, 3, 5};
    
    ​ 目标数据：
    
    存储下标的数组中内容 {0, 3, 6}；
    

**注意：**

```
1. 尾插法操作，计数器变量
2. 用于存储下标位置的新数组，容量和源数据数组一致。

```

```
class Demo11 {
	public static void main(String[] args) {
		// 1. 源数据数组
		int[] arr = {1, 1, 1, 1, 1, 1, 1, 1, 1};
		// 2. 存储下标的新数组，新数组容量和数组容量一致
		int[] newArr = new int[arr.length];
		// 3. 目标数据
		int num = 1;
		
		// 4. 定义一个变量，用于计数操作，同时满足尾插法数据存储要求
		// 【有效元素个数】
		int count = 0;
		
		// 5. 利用 for 循环找出数组中指定元素所在下标位置
		for (int i = 0; i < arr.length; i++) {
			// 6. 如果找到了目标元素，对应下标位置存储到新数组中
			if (num == arr[i]) {
				// 新数组中存储下标 i
				newArr[count] = i;
				count++;
			}
		}
		
		if (count > 0) {
			// 6. count 记录查询到的元素个数，展示下标情况
			for (int i = 0; i < count; i++) {
				System.out.println(newArr[i]);
			}
		} else {
			System.out.println("Not Found!!!");
		}
		
	}
}

```

​