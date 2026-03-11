# 数据结构

## 概论

### 数据结构

#### 数据组织、空间使用与算法效率

**数据组织：**解决问题方法效率，跟数据的组织方式有关

**空间使用：**解决问题方法效率，跟空间的利用率有关

**算法效率：**解决问题方法效率，跟算法的巧妙程度有关

#### 抽象数据类型

- 数据对象在计算机中的组织方式
  - 逻辑结构
  - 物理存储结构
- 数据对象必定与一系列加在其上的操作有关
- 完成这些操做所用的方法就是算法
- 数据类型
  - 数据对象集
  - 数据集合相关联的操作集
- 抽象：描述数据类型的方法不依赖于具体实现
  - 与存放数据的机器无关
  - 与数据存储的物理结构无关
  - 与实现操作的算法和编程语言均无关

只描述数据集和相关操作集“是什么”，并不涉及“如何做到”的问题

例：矩阵的表示

```
类型名称：矩阵
数据对象集：一个M\*N的矩阵A由M*N个三元组<a,i,j>构成，其中a是矩阵元素的值，i是元素所在的行号，j是元素所在的列号。
操作集：对于任意矩阵A，B，C∈ Matrix ，以及整数i、j、M、N
	Matrix Create(int M, int N):返回一个M*N的空矩阵
	int GetMaxRow(Matrix A ):返回矩阵A的总行数
	int GetMaxCol(Martix A ):返回矩阵A的总列数
	ElementType GetEntry ( Matrix A, int i, int j ):返回矩阵第i行、第j列的元素
	Martix Add( Martix A，Martix B):如果A和B的行、列数一致，则返回矩阵C=A+B，否则返回错误标志
	Martix Multiply( Martix A, Martix B):如果A的列数等于B的行数，则返回矩阵C=AB，否则返回错误标志
```

###  算法

#### 算法

- 一个有限的指令集
- 接受一些输入（有些情况下不需要输入）
- 产生输出
- 一定在有限步骤之后终止
- 每一条指令必须
  - 有充分明确的目标，不可有明确的歧义
  - 计算机能处理范围内
  - 描述不依赖于任何一种计算机语言以及具体的实现手段

例：选择排序算法的伪码描述

```c
void Selection( int list[], int N )
{/* 将N个整数List[0]...List[N-1]进行非递减排序*/
	for(i = 0; i < N; i ++ ) {
        MinPosition = ScanForMin( List， i ，N-1)
		/*从List[i]到List[N-1]中找最小元，并将位置赋给MinPosition*/
    	Swap( List[i], List[MinPositon])        
		/*将未排序部分的最小元换到有序部分的最后位置*/
	}
}
```

#### 算法分析 

- 时间复杂度$$T(n)$$——根据算法写成的程序在执行时耗费时间的长度。这个长度也与输入数据的规模有关。时间复杂度过高的算法可能导致内存超限，造成程序非正常中断
- 空间复杂度$S(n)$——根据算法写成的程序执行时占用的存储单元的长度。这个长度往往与输入数据的规模有关。空间复杂度过高的算法可能导致内存超限，造成程序非正常中断

例：输出指定范围的数

```c
void print(int N)
{
	int i;
	for(i=0;i<N;i++)
	{
		printf("%d\n",i);
	}
	return ;
}
```

$S(n) =C$

```c
void print(int N)
{
	if(N)
	{
	print(N-1);
	printf("%d\n",N);
	}
	return ;	
}
```

$$S(n)=C\cdot N$$

```c
void print(int N)
{
	if(N)
	{
	print(N-1);
	printf("%d\n",N);
	}
	return ;	
}
```

例：多项式计算

```c
double f(int n, double a[], double x )
{	int i;
 	double p = a[0];
    for ( i=1； i<=n; i--)
        p += (a[i] * pow(x,i));
 	return p;
}
```

$$T( n) =Cn=C_1n^2+C_2n$$

```c
double f( int n, double a[], double x )
{	int i;
 	double p = a[n];
    for ( i=n; i>0; i--)
        p = a[i-1] + x*p;
 	return p;
}
```

$$T( n) =Cn$$

#### 复杂度分析

复杂度的渐进表示法

- $$T(n)=O(f(n)) $$表示存在常数 $$C>0$$,$$n_0>0$$使得当$$n\geqslant n_0$$时有$$T(n)\leqslant C\cdot f(n)$$
- $T(n)= \varOmega(g(n))$表示存在常数$$C>0$$,$$n_0>0$$使得当$n\geqslant n_0$时有$T(n)\leqslant C\cdot g (n) $
- $T(n)=\varTheta (h(n))$表示同时有$T(n) = O(h(n))$和$T(n)=\varOmega(h(n))$

小窍门

- 若有两段算法分别有复杂度$T_1(n)=O(f_1(n))$和$T_2(n)=O(f_2(n))$，则
  - $T_1(n)+T_2()=max(O(f_1(n)),O(f_2(n)))$
  - $T_1(n) \times T_2(n)=O(f_1(n)\times f_2(n))$
- 若$T(n)$是关于$n$的$k$阶多项式，那么$T(n)=\varTheta(n^k)$ 
- 一个for循环的时间复杂度等于循环次数乘以循环体代码的复杂度
- if-else结构的复杂度取决于if的条件判断复杂度和两个分支部分的复杂度，总体复杂度取三者最大

输入规模

![image-20250415203525961](images/image-20250415203525961.png)

#### 算法应用

##### 最大子列和问题

给定$N$个整数的序列${A_1,A_2,...,A_N}$求函数$f(i,j)=max\{0,\sum A_k\}$的最大值

算法1(暴力遍历)

```c
int MaxSubseqSum1(int A[], int N)
{  	int ThisSum,MaxSum = 0;
	int i,j,k;
	for( i = 0; i < N; i++){ /*i是子列左端的位置*/
		for( j = i; j < N; j++ ) {/*j是子列右端的位置*/
			ThisSum = 0;	/*ThisSum是从A[i]到A[j]的子列和*/
			for(k = i; K <= j; k++)
				ThisSum += A[k];
			if (ThisSum > MaxSum )	/*如果得到的子列和更大*/
				MaxSum = ThisSum;	/*则更新结果*/
				}/*j循环结束*/
			}/*i循环结束*/
 	return MaxSum;
}
```

$T(N)=O(N^3)$

算法2

```c
int MaxSubseqSum2(int A[], int N)
{  	int ThisSum,MaxSum = 0;
	int i,j;
	for( i = 0; i < N; i++){ /*i是子列左端的位置*/
		ThisSum = 0;	/*ThisSum是从A[i]到A[j]的子列和*/
         for( j = i; j < N; j++ ) {/*j是子列右端的位置*/
			ThisSum += A[j];
             /*对于相同的i，不同的j，只要在j-1次循环的基础上累加1项即可*/
			if (ThisSum > MaxSum )	/*如果得到的子列和更大*/
				MaxSum = ThisSum;	/*则更新结果*/
				}/*j循环结束*/
			}/*i循环结束*/
 	return MaxSum;
}
```

$T(N)=O(N^2)$

算法3(分而治之)

![](images/image-20250415211158274.png)

$$T(N)=2T(N/2)+cN,	T(1)=O(1)\\=2[2T(N/2^2)+cN/2]+cN\\=2^kO(1)+ckN，其中N/2^k=1$$

```c
/*返回三个整数的最大值*/
int Max3 ( int A, int B, int C){
    return (A>B) ? (A>C?A:C):(B>C?B:C);
}
/*分治法求List[left]到list[right]的最大子列和*/
int DivideAndConquer (int list[], int left,int right){
    int MaxLeftSum, MaxRightSum;	//存放左右子问题的解
    int MaxLeftBorderSum , MaxRightBorderSum;	//存放跨分界线的边界
    
    int LeftBorederSum,RightBorderSum;
    int center, i;
    
    /*递归的终止条件，子列只有一个数字*/
    if(left == right){
        if( list[left]>0)	return List[left];
        else return 0;
    }
    
    /*分的过程*/
    center=(left+right)/2;//找到中分点
    MaxLeftSum = DivideAndConquer (list,left,center);//递归求左子列和
    MaxRightSum = DivideAndConquer (list,center+1,right);//递归求右子列和
    
    /*求跨分界线的最大子列和*/
    MaxLeftBorderSum = 0; LeftBorderSum=0;
    for(i =center;i>=left;i--){
        LeftBorderSum += List[i];
        if ( LeftBorderSum > MaxLeftBorderSum)
            MaxLeftBorderSum = LeftBorderSum;
    }//左边扫描结束
        
    MaxRightBorderSum = 0; RightBorderSum = 0;
    for(i = center+1;i <=right; i++){
        RightBorderSum += List[i];
        if ( RightBorderSum > MaxRightBorderSum)
            MaxRightBorderSum = RightBorderSum;
    }//右边扫描结束
        
    /*返回治的结果*/
    return Max3(MaxLeftSum ,MaxRightSum,MaxLeftBorderSum + MaxRightBorderSum)
}
/*此函数用于保持接口相同*/
int MaxSubseqSum3(int A[], int N){
    return DivideAndConquer ( List, 0, N-1);
	}
```

$T(n)=O(n\log n)$

算法4(在线处理)

```c
int MaxSubseqSum4(int A[], int N)
{	int ThisSum, MaxSum;
	int i;
	ThisSum = MaxSum = 0;
	for( i = 0; i < N; i++){
		ThisSum += A[i];	/*向右累加*/
		if(ThisSum > MaxSum)
			MaxSum = ThisSum;	/*发现更大和则更新当前结果*/
		else if(ThisSum < 0)	/*如果当前子列和为负*/
			ThisSum = 0;	/* 则不可能是后面部分和增大，抛弃之*/
	}
	return MaxSum;
}
```

$T(N)=O(N)$

"在线"的意思是指每输入一个数据就进行即时处理，在任何一个地方终止输入，算法都能正确给出当前的解

## 线性结构

### 线性表

#### 多项式表示

[例]一元多项式及其运算

一元多项式：$f(x)=a_0+a_1x+...+a_{n-1}x^{k-1}+a_nx^k$

主要运算：多项式相加、相减、相乘等

[分析]如何表示多项式

多项式的关键数据：

- 多项式项数$n$
- 各项系数$a_i$及指数$i$

方法1：顺序存储结构的直接表示0

数组各分量对应多项式各项：

a[i]:项xi的系数ai

例如：$f(x)=4x^5-3x^2+1$

表示成：

![image-20250416195214995](C:\Users\liyao\AppData\Roaming\Typora\typora-user-images\image-20250416195214995.png)









两个多项式相加：对应数组的分量相加

方法2：顺序存储结构表示非零项

每个非零项$a_ix^i$涉及两个信息：系数$a_i$和指数$i$

可以将每一个多项式看成一个$(a_i,i)$二元组集合

用结构数组表示：数组分量是由系数$a^i$、指数$i$组成的结构，对应一个非零项

按指数大小有序存储！

相加过程：从头开始，比较两个多项式当前项的指数

方法3：

链表中每个结点存储多项式的一个非零项，包括系数和指数两个数据域以及一个指针域

| coef | expon | link |
| ---- | ----- | ---- |
| 系数 | 指数  | 指针 |

```c
typedef struct PolyNode *Polynomial;
struct PolyNode{
    int coef;
    int expon;
    Polynomial link;
}
```

例如：

$P_1(x)=9x^12+15x^8+3x^2$

$P_2(x)=26x^{19}-4x^8-13x^6+82$

链表存储形式为：

![image-20250416201355998](images/image-20250416201355998.png)

#### 线性表及顺序存储

##### 多项式问题启示

1. 同一个问题可以有不同的表示及（存储）方法
2. 有一类共性问题：有序线性序列的组织和管理

##### 线性表

“线性表（Linear List）”：是由同类型数据元素构成有序序列表的线性结构

- 表中元素的个数称为线性表的长度
- 线性表没有元素时，称为空表
- 表起始位置称为表头，表结束的位置称为表尾

##### 线性表的抽象数据类型描述
```
类型名称：线性表（List）
数据对象集：线性表是n(≥0)个元素构成的有序序列(a1,a2,……,an)
操作集：线性集L∈List，整数i表示位置，元素X∈ElementType，线性表基本操作主要主要有：

1、ListMakeEmpty():初始化一个空线性表L;
2、ElementType FindKth (int K,List L):根据位序K,返回相应元素;
3、int Find(ElementType X,List L):在线性表L中查找X第一次出现的位置;
4、void Insert(ElementType X,int i,List L):在位序之前插入一个新元素X;
5、void Delete(int i,List L):删除指定位序i的元素;
6、int Length(List L):返回线性表L的长度n。
```

##### 线性表的顺序存储实现

利用数组的连续存储空间顺序存放线性表的个元素

| 下标i | 0     | 1     | ……   | i-1   | i         | ………  | n-1   | ……   | MAXSIZE-1 |
| ----- | ----- | ----- | ---- | ----- | --------- | ---- | ----- | ---- | --------- |
| Data  | $a_1$ | $a_2$ | ……   | $a_i$ | $a_{i+1}$ | ………  | $a_n$ | ……   | -         |

```c
typedef struct LNode *List;
struct LNode{
    ElementType Data[MAXSIZE];
    int Last;
};
struct Lnode L;
List PtrL
```

访问下标为i的元素：L.Data[i]或PtrL->Data[i]

线性表的长度：L.Last+1或PtrL->Last+1

主要操作的实现

1. 初始化

```c
List MakeEmpty()
{	List PtrL;
    PtrL = (List)malloc(sizeof(struct LNode));
 	PtrL->Last = -1;
 	return PtrL;
}
```

2. 查找

   ```c
   int Find (ElementType X,List PtrL)
   {	int i = 0;
    	while(i <= PtrL->Last && PtrL -> Data[i]!= X)
           i++;
    	if (i > PtrL -> Last) return -1; /*如果没找到，返回-1*/
       else return i;					/*找到后返回的是存储位置*/
   }
   ```

   查找成功的平均比较次数为$(n+1)/2$,平均时间性能为$O(n)$。

3. 插入操作实现

   ```c
   void Insert(ElementType X,int i,List PtrL)
   {	int j;
    	if(PtrL->Last == MAXSIZE-1){/*表空间已满，不能插入*/
           printf("表满");
           return ;
       }
       if(i<1|| i>PtrL->Last+2){/*检查插入位置的合法性*/
           printf("位置不合法");
           return;
       }
    	for(j=PtrL->Last;j>=i-1;j--)
           PtrL->Data[j+1] = Ptrl -> Data[j];/*将ai~an倒序向后移动*/
    	Ptrl->Data[i-1] = X;				/*新元素插入*/
    	PtrL->Last++;						/*Last仍指向最后元素*/
    	return; 
   }
   ```

   查找成功的平均比较次数为$n/2$,平均时间性能为$O(n)$。

4. 删除（删除表的第$i(l\leqslant i \leqslant n)$个位置上的元素）

   ![](images/image-20250416213533254.png)

   ```c
   void Delete(int i,List PtrL)
   {	int j;
    if(i<1 || i>PtrL->Last+1){/*检查空表及删除位置的合法性*/
        printf("不存在第%d个元素",i);
        return ;
    }
    for(j=i;j <= PtrL->Last;j++)
    	PtrL->Data[j-1] = PtrL->Data[j];/*将a+1~an顺序向前移动*/
    PtrL->Last--;						/*Last仍指向最后元素*/
    return;
   }
   ```

##### 线性表的链式存储实现

​	不要求逻辑上相邻的两个元素相邻；通过“链”建立起数据之间的逻辑关系。

- 插入、删除不需要移动数据元素，只需要修改“链”

![image-20250416221005000](images/image-20250416221005000.png)

```c
typedef struct LNode *List;
struct LNode {
    ElementType Data;
    List Next;
};
struct LNode L;
List PtrL;
```

主要操作的实现

1. 求表长

   ```c
   int Length(List PtrL)
   {	List p= PtrL;
   	int j= 0; 
   	while(p){
   		p=p->Next;
   		j++;
   	}
   	return j;
   }
   ```

   时间性能为$O(n)$

2. 查找

   （1）按序号查找：FindKth

   ```c
   List FindKth(int K,List PtrL) 
   { 	List p=PtrL;
       int i;
    	while(p!=NULL && i<K){
           p=p->Next;
           i++;
       }
       if (i==K) return p;
    		/*找到第K个，返回指针*/
    	else return NULL;
    		/*否则返回空*/
   }
   ```

   （2）按值查找：Find

   ```c
   List Find(ElementType X,List PtrL)
   {
       List p= PtrL;
       while(p!=NULL && p->Data != X)
           p = p->Next;
       return p;
   }
   ```

3. 插入（在第$i-1(1\leqslant i \leqslant n+1)$）个结点后插入一个值为X的新结点0

   1.  先构造一个新结点，用$s$指向；

   2. 再找到链表的第$i-1$个结点，用$p$指向

   3. 然后修改指针，插入结点($p$之后插入的新结点是s)；

      ![image-20250417190735110](images/image-20250417190735110.png)

      ```c
      List Insert(ElementType X,int i, List PtrL)
      {	List p,s;
      	if (i==1){//新结点插入在表头
              s=(List)malloc(sizeof(struct LNode));//申请、填装结点
              s->Data = X;
              s->Next = PtrL;
              return s;//返回新表头指针
          }
      	p=FindKth(i-1,PtrL);//查找第i-1个结点
      	if(p==NULL){//第i-1个不存在，不能插入
              printf("i");
              return NULL;
          }else{
              s=(list)malloc(sizeof(struct LNode));//申请、填装结点
              s->Data = X;
              s->Next = p->Next;//新结点插入在第i-1个结点后面
              p->Next = s;
              return PtrL;
          }}
      ```

      

4.  删除（删除链表的第$i(1\le i \le n)$个位置上的结点）

   1. 先找到链表上第$i-1$个结点，用$p$指向；
   2. 在用指针s指向要被删除的结点（$p$的下一个结点）；
   3. 然后修改指针，删除$s$所至的结点；
   4. 最后释放所指结点的空间。

   ![image-20250417192701362](images/image-20250417192701362.png)

   ![image-20250417192729651](images/image-20250417192729651.png)

   ```c
   List Delete(int i,List PtrL)
   {	List p,s;
       if(i==1){//若要删除的是表的第一个结点
           s=PtrL;//s指向第一个结点
           if(PtrL!=NULL) PtrL =PtrL->Next;//从链表中删除
           else return NULL;
           free(s);//释放被删除结点
           return PtrL;
       }
    	P=FindKth(i-1,PtrL);//查找第i-1个结点
    	if(p==NULL){
   	printf("%d",i-1);	return NULL;
       }else if (p->Next == NULL){
           printf("%d",i);	return NULL;
       } else{
   		s=p->Next;//s指向第i个结点
       	p->Next=s->Next;//从链表中删除
           free(s);//释放被删除结点
           return PtrL;
           
       }
   	
       
   }
   ```

#### 广义表（Generalized List）

- 广义表是线性表的推广
- 对于线性表而言，那个元素都是基本单元素
- 广义表中，这些元素不仅是单元素也可以是另一个广义表。

```c
typedef struct GNode *Glist;
struct GNode{
    int Tag;//标志域：0表示结点是单元素，1表示结点是广义表
    union {//子表指针域Sublist域氮元素数据与Data复用，及工业存储空间
	ElementType Data;
    Glist SubList;
    }URegion;
    Glist Next;//指向后继结点
};
```

![image-20250417201151192](images/image-20250417201151192.png)

#### 多重链表

多重链表：链表中的结点可能隶属于多个链

- 多种链表中结点的指针域会有多个，如前面例子包含了Next和SubList两个指针域；
- 但包含两个指针域的链表不一定是多重链表，比如在双向链表不是多重链表

多重链表有广泛的用途：基本上如树、图这样相对复杂的数据结构可以采用多重链表方式实现存储

[例]矩阵可以用二维数组表示，但二维数组表示有两个缺陷

- 一是数组大小需要事先确定，
- 对于"稀疏矩阵",将造成大量的存储空间浪费。

[分析]采用一种典型的多重链表——十字链表来存储稀疏矩阵

- 只存储矩阵非零元素项

  节点的数据域：行坐标Row，列坐标Col，数值Value

- 每个结点通过两个指针域，把同行、同列串起来；

  - 行指针（或称为右指针）Right
  - 列指针（或称为下指针）Down

![image-20250417221357809](images/image-20250417221357809.png)

- 用一个标识域Tag来区分头节点和非0元素结点
- 头节点的标识值为"Head",矩阵非0元素结点的标识符为"Term"。

![image-20250417222440587](images/image-20250417222440587.png)

### 堆栈

算术表达式5+6/2-3*4。正确理解：

5+6/2-3*4=5+3-3\*4=8-3\*4=8-12=-4

- 有两类对象构成：
  - 运算数，如2、3、4
  - 运算符号，如+、-、*、/
- 不同算术符号的优先级不同

后缀表达式

- 中缀表达式：运算符号位于两个运算数之间。如，a+b*c-d/e
- 后缀表达式：运算符号位于两个运算数之后。如，abc*+de/-

后缀表达式求值策略：从左到右“扫描”，逐个处理运算数和运算符号

1. 遇到运算数怎么办？如何”记住“目前还未参与运算的数？
2. 遇到运算符号怎么办？对应的运算数是什么?

启示：

需要有种存储方法，能顺序存储运算数，

并在需要时”倒序”输出！

![image-20250418210133124](images/image-20250418210133124.png)
$T(n)=O(n)$

#### 堆栈的抽象数据类型描述

堆栈（Stack）：具有一定操作约束的线性表

- 只在一端（栈顶，Top）做插入、删除

- 出入数据：入栈（Push）
- 删除数据：出栈（Pop）
- 后入先出：Last In First Out （LIFO）

```
类型名称：堆栈(Stack)

数据对象集：一个有0个或多个元素的有穷线性表

操作集：长度为MaxSize的堆栈S∈Stack，堆栈元素item∈ElementType

1、Stack CreateStack(int MaxSize):生成空堆栈，其最大长度为MaxSize;
2、int IsFull(Stack S,int MaxSize):判断堆栈S是否已满;
3、void Push(Stack S,ElementType item):将元素item压入堆栈;
4、int IsEmpty(Stack S):判断堆栈S是否为空;
5、ElementType Pop(Stack S):删除并返回栈顶元素；
```

![image-20250418213025696](images/image-20250418213025696.png)

Push和Pop可以穿插交替进行：

#### 栈的顺序存储实现

​	栈的顺序存储结构通常由一个一维数组和一个记录栈顶元素位置的变量组成。

```c
#define MaxSize <存储数据元素的最大个数>
typedef struct SNode *Stack;
struct SNode{
    ElementType Data[MaxSize];
    int Top;
}
```

1. 入栈

   ```c
   void Push (Stack PtrS,ElementType item)
   {
       if(PtrS->Top == MaxSize-1){
           printf("堆栈满");return;
       }else{
           PtrS->data[++(PtrS->Top)] = item;
           return;
       }
   }
   ```

   {PtrS->data[++(PtrS->Top)] = item;}=={(PtrS->Top)++;PtrS->Data[PtrS->Top]=item;}

2. 出栈

   ```c
   ElementType Pop(Stack PtrS)
   {
   	if(PtrS->Top==-1){
           printf("堆栈空");
           return ERROR;//ERROR是ElementType的特殊值，标志错误
       } else
           return (PtrS->Data[(PtrS->Top)--]);
   }
   ```

【例】

请用一个数组实现两个堆栈，要求最大地利用数组空间，使用数组只要有空间入栈操作就可以成功

【分析】

一种比较聪明的办法是使这两个栈分别从数组的两头开始向中间生长；当两个栈的栈顶针相遇时就代表两个栈都满了。

```c
#define MaxSize<存储元素的个数>
struct DStack{
    ElementType Data[MaxSize];
    int Top1;//堆栈1的栈顶指针
    int Top2;//堆栈2的栈顶指针
}S;
S.Top1=-1;
S.Top2=MaxSize;
```

```c
void Push(struct DStack *PtrS,ElementType item ,int Tag)
{//Tag作为区分两个堆栈的标志，取值为1和2
    if(PtrS->Top2-PtrS->Top1==1){//堆栈满
        printf("堆栈满");return;
    }
    if(Tag==1)//对第一个堆栈操作
        PtrS->Data[++(PtrS->Top1)]==item;
    else//对第二堆栈操作
        PtrS->Data[--(PtrS->Top2)]==item;
}
ElementType Pop(struct DStack *PtrS,int Tag)
{//Tag作为区分两个堆栈的标志，取值为1和2
    if(tag==1){//对第一个堆栈操作
		if(PtrS->Top1==-1){//堆栈1空
            printf("堆栈1空");return NULL;
        }else return PtrS->Data[(PtrS->Top1)--];
    }else{//对第二个堆栈操作
        if(PtrS->Top2==MaxSize){//堆栈2空
            printf("堆栈2空"),return NULL;
        }else return PtrS->Data[(PtrS->Top2)++];
    }
}
```

#### 堆栈的链式存储实现

栈的链式存储结构实际上就是一个指针，叫做链栈。插入和删除操作只能在链栈的栈顶进行。

```c
typedef struct SNode *Stack;
struct SNode{
    ElementType Data;
    struct SNode *Next;
};
```

1. 堆栈的初始化（建立空栈）
2. 判断堆栈S是否为空

```c
Stack CreateStack()
{//构建一个堆栈的头节点，返回指针
    Stack S;
    S=(Stack)malloc(sizeof(struct SNode));
    S->Next = NULL;
    return S;
}

int IsEmpty(Stack S)
{//判断堆栈S是否为空，若为空函数返回整数1，否则返回0
    return (S->Next == NULL);
}

void Push(ElementType item,Stack S)
{//将元素item压入堆栈S
    struct SNode *TmpCell;
    TmpCell=(struct SNode *)malloc(sizeof(struct SNode));
    TmpCell->Element = item;
    TmpCell->Next = S->Next;
    S->Next = TmpCell;
}

ElementType Pop(Stack S)
{//
    struct SNode *FirstCell;
    ElementType TopElem;
    if(IsEmpty(S)){
        printf("");return NULL;
    }else{
		FirstCell = S->Next;
    	S->Next = FirstCell->Next;
    	TopElem = FirstCell->Element;
    	free(FirstCell);
    	return TopElem;
    }
}
```

#### 堆栈的应用：

##### 表达式的求值:中缀表达式求值

基本策略：将中缀表达式转化为后缀表达式，然后求值

1. 运算数的相对顺序不变
2. 运算符号的顺序发生改变（堆栈）
   - 需要存储“等待中”的运算符号
   - 需要当前运算符号与“等待中”的最后一个运算符号比较

中缀表达式如何转化为后缀表达式

- 从头到尾读取中缀表达式的每个对象，对不同对象按不同情况处理。

1. 运算数：直接输出
2. 左括号：压入堆栈
3. 右括号：将栈顶的运算符弹出并输出，知道遇到左括号（出栈，不输出）
4. 运算符：
   - 若运算符大于栈顶运算符时，则把它压栈
   - 若优先级小于栈顶的运算符时，将栈顶运算符弹出并输出；在比较新的栈顶运算符，直到该运算符大于栈顶运算符的优先级为止，然后将该运算符压栈
5. 若各对象处理完毕，则把堆栈存留的运算符一并输出

##### 其他应用

- 函数调用及递归调用
- 深度优先搜索
- 回溯算法

### 队列

队列（queue）：具有一定操作约束的线性表

​		插入和删除操作：只能在一端插入，而在另一端删除

- 数据插入：入队列（AddQ）
- 数据删除：出队列（DeleteQ）
- 先来先服务
- 先进先出：FIFO

#### 队列的抽象数据类型描述

```
类型名称：队列（Queue）

数据对象集：一个有0个或多个元素的又穷线性表

操作集：长度为MaxSize的队列Q∈Queue，队列元素item∈ElementType

1、Queue CreateQueue(int MaxSize):生成长度为MaxSize的空队列
2、int IsFullQ(Queue Q,int MaxSize):判断队列Q是否已满
3、void AddQ(Queue Q,ElementType item):将数据元素item插入队列Q中
4、int IsEmptyQ(Queue Q):判断队列Q是否为空
5、ElementType DeleteQ(Queue Q):将队头数据元素从队列中删除并返回
```

#### 队列的顺序存储实现

​	队列的顺序存储结构通常由一个一维数组和一个记录队列头元素位置的变量front以及一个记录队列尾元素位置的变量rear组成。

```c
#define MaxSize <存储数据元素的最大个数>
struct QNode{
    ElementType Data[MaxSize];
    int rear;
    int front
}
typedfe struct QNode *Queue
```

单向队列

![image-20250422194557376](images/image-20250422194557376.png)

顺环队列

![image-20250422194831318](images/image-20250422194831318.png)

判断堆栈空还是满

解决方案：

1. 使用额外标记：Size或者tag域
2. 仅使用n-1个数组空间

1. 入队列

   ```c
   void AddQ(Queue PtrQ,ElementType item)
   {
       if ((PtrQ->rear+1)%MaxSize == PtrQ -> front ){
           printf("队列满");
           return;
       }
       PtrQ->rear=(PtrQ->rear+1)%MaxSize;
       PtrQ->Data[PtrQ->rear] = item;
   }
   ```

2. 出队列

   ```c
   ElementType DeleteQ(Queue PtrQ)
   {
       if(PtrQ->front==PtrQ->rear){
           printf("队列空");
           return ERROR;
       }else{
           PtrQ->front=(PtrQ->front+1)%MaxSize;
       	return PtrQ->Data[PtrQ->front];
       }
   }
   ```

#### 队列的链式存储实现

队列的链式存储结构可以使用一个单链表实现。插入和删除操作分别在链表的两头进行

![image-20250422201525769](images/image-20250422201525769.png)

```c
bustruct Node{
    ElementType Data;
    struct Node *Next;
};
struct QNode{//链队列结构
    struct Node *rear;//指向队尾结点
    struct Node *front;//指向队头结点
};
typedef struct QNode *Queue;
Queue PtrQ;
```

不带头结点的链式队列出队操作的一个示例：

```c
ElementType DeleteQ(Queue PtrQ)
{	
    struct Node *FrontCell;
    ElementType FrontELem;
 	
 	if (PtrQ->front == NULL){
        printf("");return ERROR;
    }
 	FrontCell = PtrQ->front;
 	if(PtrQ->front==PtrQ->rear)
        PtrQ->front==PtrQ->rear=NULL; 	
    else
        PtrQ->front==PtrQ->front->Next;
    FrontElem = FrontCell->Data;
    free(FrontCell);
    return FrontElem;
    
}
```

#### 队列的应用

##### 多项式加法运算

主要思路：相同指数的项系数相加，其余部分拷贝

采用不带头结点的单向链表，按照指数递减的顺序排列各项

```c
struct PolyNode{
    int coef;//系数
    int expon;//指数
    struct PolyNode *link;//指向下一个节点的指针
};
typedef struct PolyNode *Polynomial;
Polynomial P1,P2;
```

算法思路：将两个指针P1和P2分别指向两个多项式第一个的节点，不断循环：

- P1->expon==P2->expon:系数相加，若结果不为0，则作为结果多项式对应项的系数。同时P1和P2分别指向下一项；
- P1->expon>P2->expon:将P1的当前项存入结果多项式，并使P1指向下一项
- P1->expon\<P2->expon:将P2的当前项存入结果多项式，并使P2指向下一项

当某一多项式处理完时，将另一个多项式的所有结点依次复制到结果多项式中去

```c
Polynomial PolyAdd(Polynomial P1,Polynomial P2)
{
    Polynomial front,rear,temp;
    int sum;
    rear = (Polynomial)malloc(sizeof(struct PolyNode));
    front = rear;//由front记录结果多项式链表头结点
    while(P1&&P2)//当两个多项式都有非零项待处理时
        switch (Compare(P1->expon,P2->expon)){
            case 1:
                Attach(P1->coef,P1->expon,&rear);
                P1=P1->link;
                break;
            case -1:
                Attach(P2->coef,P2->expon,&rear);
                P2=P2->link;
                break; 
            case 0:
                sum=P1->coef+P2->coef;
                if(sum)Attach(sum,P1->expon,&rear);
                P1=P1->link;
                P2=P2->link;
                break;
        }
    //将未处理完的里一个多项式的所有节点一次复制到结果多项式中去
    for(;P1;P1=P1->link)Attach(P1->coef,P1->expon,&rear);
    for(;P2;P2=P2->link)Attach(P2->coef,P2->expon,&rear);
    rear->link=NULL;
    temp=front;
    front=front->link;//令front指向结果多项式第一个非零项
    free(temp);//释放临时空表头结点
    return front
}
void Attach(int c,int e,Polynomial *pRear)
{
    Polynoimal P;
    p->coef = c;//对新结点赋值
    p->expon = e,
    p->link=NULL;
    (*pRear)->link = P;
    *pRear = P;//修改pRear值
}
```

### 例：多项式乘法与加法

仅表示非零项

数组：

编程简单、调试容易

需要实现确定数组大小

链表：

动态性强

编程略微复杂，调试较为困难

一种比较好的实现方法是动态数组

数据结构设计

```c
typedef struct PolyNode *Polynomial;
struct PolyNode{
    int coef;
    int expon;
    Polynomial link;
};
```

程序框架搭建

```c
int main(){
    Polynomial P1,P2,PP,PS;
    
    P1=ReadPoly();
    P2=ReadPoly();
    PP=Mult(P1,P2);
    PrintPoly(PP);
    PS=Add(P1,P2);
    PrintPoly(PS);
    
    return 0;
}
```

读入多项式

```c
Polynomial ReadPoly()
{
	PolyNomial P ,Rear,t;
    inr c, e,N;
    scanf("%d",&N);
    P=(Polynomial)malloc(sizeof(struct PolyNode));//
    P->link=NULL;
    Rear=P;
    while(N--){
	scanf("%d %d",&c,&e);
        Attach(c,e,&rear)
    }
    t=P;P=P->link;free(t);
    return P;
}
```

Rear初值为多少：

1. Rear初值为NULL
2. Rear指向一个空节点

```c
void Attach(int c,int e,Polynomial *pRear)
{	
    Polynomial P;
    P=(polynomial)malloc(sizeof(struct PolyNode));
    p->coef = c;//对新结点赋值
 	p->expon=e;
	p->link=NULL;
    (*pRear)->link=P;
    *pRear=P;//修改pRear的值
}
```

将两个多项式相加

```c
Polynomial Add (Polynomial P1,Polynomial P2)
{
    t1=P1;t2=P2;
    P=(Polynomial)malloc(sizeof(struct Polynomial));P->link=NULL;
    Rear = P;
    while(t1&&t2){
        if(t1->expon==t2->expon)
        {
            
        }else if (t1->expon >t2->expon){
            
        }
        else{
            
        }
    }
    while (t1){
        
    }
    while(t2){
        
    }
    return P;
```

将两个多项式相乘

方法：

将乘法运算转换为加法运算

将P1当前项（ci,ei）乘P2多项式，再将结果加到多项式里

```c
t1=P1;t2=P2;
P=(Polynomial)malloc(sizeof(struct PolyNode));P->link =NULL;
Rear = P;
while (t2){
    Attach(t1->coef*t2->coef,t1->expon+t2->expon,&Rear);
    t2=t2->link
}
```

1. 逐项插入

   ​	将P1当前项$(c_{1i},e_{1i})$乘P2当前项$(c_{2i}+e_{2i})$,并插入结果多项式中。关键是要找到插入位置

   ​	初始结果多项式可由P1第一项乘P2获得(如上)

```c
Polynomial Mult(Polynomial P1,Polynomial P2)
{
    Polynomial P,Rear,t1,t2,t;
    int c,e;
    
    if(!P1||!P2)return NULL;
    
    t1=P1;t2=P2;
    P=(Polynomial)malloc(sizeof(struct PolyNode));P->link=NULL;
    Rear=P;
    while(t2)
    {
        Attach(t1->coef*t2->coef,t1->expon+t2->expon,&Rear);
        t2=t2->link
    }
    t1=t1->link;
    while(t1)
    {
        t2=P2;Rear = P;
        while(t2){
            e=t1->expon+t2->expon;
            c=t1->coef*t2->coef;
            while(Rear->link&&Rear->link->expon>e)
                Rear=Rear->link;
            if(Rear->link&&Rear->link->expon==e){
                if(Rear->link->coef+c)
                    Rear->link->coef+=c;
                else{
                    t=Rear->link;
                    Rear->link=t->link;
                    free(t);
                }
            }
            else{
                t=(Polynomial)malloc(sizeof(struct PolyNode));
                t->coef=c;t->expon=e;
                t->link =Rear->link;
                Rear->link=t;Rear=Rear->link;
            }
            t2=t2->link;
        }
        t1=t1->link;
    }
    t2=P;P=P->link;free(t2);
    return P;
}
```

将多项式输出

```c
void PrintPoly(Polynomial P)
{//输出多项式
    int flag=0;
    
    if(!P){printf("0 0\n");return;}
    
    while(P){
        if(!flag)
            flag = 1;
        else:
        	printf("");
        printf("%d %d",P->coef,P->expon);
        P=P->link;
    }
}
```

### 例：反转链表

#### 抽象链表

- 有块地方存数据
- 有块地方存指针——下一个结点的位置

#### 单链表逆转

![image-20250423204215564](images/image-20250423204215564.png)

取巧：

用顺序表存储，先排序，在直接逆序输出

```c
Ptr Reverse (Ptr head,int K ){
    cnt = 1;
    new = head->next;
    old = new->next;
    while(cnt<K){
        tmp=old->next;
        old->next = new;
        new = old; old = tmp;
        cnt ++;
    }
    head->next->next = old;
    return new;
}
```

## 树

### 树

#### 顺寻查找

客观世界中许多事物存在层次关系

分层次组织在管理上具有更高的效率

数据管理的基本操作之一查找

##### 查找

查找：根据某个给定关键字K，从集合R中找出关键字与K相同的记录

静态查找：集合中的记录是固定的

- 没有插入与删除操作，只有查找

动态查找：集合中记录是动态变化的’

- 除查找，还可能发生插入和删除

##### 静态查找

```c
int SequentialSearch(List Tbl,ElementType K)
{//在Element[1]~Element[n]中查找关键字为K的数据元素
    int i;
    Tbl -> Element[0]=K;//建立哨兵
    for(i=Tbl->length;Tbl->Element[i]!=K;i--);
    return i;//查找成功并返回所在单元下标；不成功返回0
}
```

```c
typedef struct LNode *List;
struct LNode{
    ELementType Element[MAXSIZE];
    int Length
};
```

#### 二分查找

假设n个数据元素的关键字满足有序（比如：小到大）

$K_1<K_2<...<K_n$

并且连续存放（数组），那么就可以进行二分查找

```c
int BinarySearch(List Tbl,ElemenntType K)
{//在表Tbl中查找关键字为K的数据元素
    int left,right,mid,NoFound=-1;
    
    left =1;//初始左边界
    right = Tbl->Length;//初始右边界
    while(left<=right)
    {
        mid=(left+right)/2;//计算中间元素坐标
        if(K<Tbl->Element[mid])	right=mid-1;//调整右边界
        else if(K > Tbl -> Element[mid]) left=mid+1;//调整左边界
        else return mid;//查找成功，返回数据元素的下标
    }
    return NotFound;//查找不成功，返回-1
}
```

##### 判定树

![image-20250423215116888](images/image-20250423215116888.png)

- 判定树上每个结点需要的查找次数刚好为该节点所在的层数
- 查找成功是查找次数不会超过判定树的深度
- n个结点的判定树的深度为$[log_2n+1]$
- ASL=(4*4+4\*3+2\*2+1)/11=3

#### 树的定义和术语

树（Tree）：n（$n\ge0 $）个结点构成的有限集合。

当n=0时，称为空树；

对于任一可非空树（$n>0$）,它具备以下性质：

- 树中有一个称为“根（Root）”的特殊节点，用r表示
- 其余节点可分为m（$m>0$）个互不相交的有限集$T_1,T_2,...,T_m$其中每个集合本身又是一棵树，称为原来树的子树“（SubTree）”

![image-20250423220741576](images/image-20250423220741576.png)

树的基本术语

1. 结点的度(Degree)：结点的子树个数
2. 树的度：树的所有结点中最大的度数
3. 叶节点（Leaf）：度为0的结点
4. 父节点（Parent）：有子树的结点是其子树的根节点的父节点
5. 子节点（Child）：若A结点是B结点的父结点，则称B结点是A结点的字结点；子节点也称为孩子结点
6. 兄弟节点（Sibling）：具有统一父节点的各结点彼此是兄弟结点
7. 路径和路径长度：从结点$n_1$到$n_k$为一个结点序列$n_1,n_2,...,n_k,n_i$是$n_{i+1}$的父结点。路径所包含边的个数为路径的长度
8. 祖先阶段（Ancestor）：沿树根到某一结点路径上的所有结点都是这个结点的祖先结点
9. 子孙节点（Descendant）：某一结点的子树中的所有结点都是这个结点的子孙
10. 结点的层次（Level）：规定根结点在1层，其他任意结点的层数是其父节点的层数+1
11. 树的深度（Depth）：树中所有结点中最大的层次是这棵树的深度。

![image-20250423221648607](images/image-20250423221648607.png)

#### 树的表示

##### 儿子-兄弟表示法

![image-20250424185915003](images/image-20250424185915003.png)

旋转45°后形成二叉树

![image-20250424190112666](images/image-20250424190112666.png)

### 二叉树

#### 二叉树的性质及定义

二叉树T：一个有穷的结点集合

- 这个集合可以为空
- 若不为空，则他是由根节点和称为其左子树$T_L$和右子树$T_R$的两个互补交叉的二叉树组成

二叉树的五种基本形态

![image-20250424190822836](images/image-20250424190822836.png)

二叉树的子树有左右之分

![image-20250424190913849](images/image-20250424190913849.png)

特殊二叉树

- 斜二叉树（Skewed Binary Tree）

    ![image-20250424191801218](images/image-20250424191801218.png)

- 完美二叉树（Perfect Binary Tree）<br>满二叉树（Full Binary Tree）

    ![image-20250424191900811](images/image-20250424191900811.png)

- 完全二叉树（Complete Binary Tree）

    有n个结点的二叉树，对树中结点按从上至下、从左到右的顺序进行编号，编号为i（$1\le i\le n$）结点与满二叉树中位置相同

![image-20250424191954991](images/image-20250424191954991.png)

完全二叉树

![image-20250424192050436](images/image-20250424192050436.png)

非完全二叉树

二叉树几个重要性质

- 一个二叉树第i层的最大结点数为：$2^{i-1},i\ge 1$
- 深度为看的二叉树有最大结点的总数为：$2^{k}-1,k\ge1$
- 对任何非空二叉树T，若$n_0$表示叶结点的个数、$n_2$是度为2的非叶结点个数，那么两者满足的关系$n_0=n_2+1$

#### 二叉树的抽象数据类型定义

```
类型名称：二叉树
数据对象集：一个有穷节点集合
	若不为空，则由根节点何其左、右二叉子树构成
	
操作集：BT∈BinTree，item∈ElementType，重要操作有：
	1、Boolean IsEmpty(BinTree BT): 判别BT是否为空
	2、void Traversal(BinTree BT):遍历，按某顺序访问每个结点
	3、BinTree CreatBinTree():创建一个二叉树
```

常用的遍历方法有

```
void PreOrderTraversal(BinTree BT):先序——根、左子树、右子树
void InOrderTraversal(BinTree BT):中序——左子树、根、右子树
void PostOrderTraversal(BinTree BT):后序——左子树、右子树、根
void LevelOrderTraversal(BinTree BT):层次遍历，从上到下，从左到右
```

#### 二叉树的存储结构

1. 顺序存储结构

    完全二叉树：按照从上至下从左到右顺序存储n个结点的完全二叉树的结点父子关系

    - 非根节点（序号i>1）的父节点的序号是[i/2];
    - 结点（序号为i）的左孩子结点的序号是2i，（若2i<=n,否则没有左孩子）；
    - 结点（序号为i）的右孩子结点的序号是2i+1，（若2i+1<=n,否则没有右孩子）；

    ![image-20250424195759567](images/image-20250424195759567.png)

    | 结点 | A    | B    | O    | C    | S    | M    | Q    | W    | K    |
    | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | 序号 | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |

    - 一般二叉树也可以次啊用这种结构，但会造成空间浪费

    ![image-20250424200243099](images/image-20250424200243099.png)

    | 结点 | A    | B    | O    | ∧    | ∧    | M    | ∧    | ∧    | ∧    | ∧    | ∧    | ∧    | C    |
    | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | 序号 | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   |

2. 链表存储

    ```c
    typedef struct TreeNode *BinTree;
    typedef BinTree Position;
    srtuct TreeNode {
        ElementType Data;
        BinTree Left;
        BinTree Right;
    }
    ```

    ![image-20250424200933407](images/image-20250424200933407.png)

    ![image-20250424200955346](images/image-20250424200955346.png)

#### 二叉树的遍历

##### 先序遍历

遍历过程为：

1. 方位根节点
2. 先序遍历其左子树
3. 先序遍历其右子树

```c
void PreOrderTraversal(BinTree BT)
{
    if(BT){
        printf("%d",BT->Data);
        PreOrderTraversal(BT->Left);
        PreOrderTraversal(BT->Right);
    }
}
```

![image-20250424201455762](images/image-20250424201455762.png)

A(BDFE)（CGHI）

先序遍历=> 	A B D F E C G H I

##### 中序遍历

遍历过程为：

1. 中序遍历其左子树
2. 访问根结点
3. 中序遍历器右子树

```c
void InOrderTraversal(Bin Tree)
{
    if(BT){
        InOrderTraversal(BT->left);
        printf("%d",Bt->Data);
        InOrderTraversal(Bt->Right);
    }
}
```

(D B E F)A(G H C I)

中序排列=> 	D B E F A G H C I

![image-20250424204939547](images/image-20250424204939547.png)

##### 后序遍历

遍历过程为：

1. 后序遍历其左子树
2. 后续遍历器右子树
3. 访问其根节点

```c
void PostOrderTraversal(BinTree BT)
{
    if(BT){
        PostOrderTraversal(BT->Left);
        PosrOrderTraversal(BT->Right);
        printf("%d",Bt->Data);
    }
}
```

(DEFB)(HGIC)A

后序遍历=>		D E F B H G I C A

![image-20250424205626504](images/image-20250424205626504.png)

- 先序、中序和后序遍历过程：遍历过程中经过结点的路线一样，只是访问各结点的实际不同
- 图中在从入口到出口的曲线上用⨂、☆和▲三种符号分别标记出先序、中序、后序访问各结点的时刻

![image-20250424210233583](images/image-20250424210233583.png)

##### 非递归遍历

中序遍历非递归遍历算法

非递归算法实现的基本思路：使用堆栈

- 遇到一个结点，就把它压栈，并去遍历它的左子树；
- 当左子树遍历结束后，从栈顶弹出这个结点并访问它；
- 然后按其右指针再去遍历该节点的右子树

```c
void InOrderTraversal(BinTree BT)
{
    BinTree T=BT;
    Stack S = CreatStack(MaxSize);//创建并初始化堆栈S
    while(T|| !IsEmpty(S)){
        while(T){//一直向左并将沿途结点压入堆栈
            Push(S,T);
            T = T->left;
        }
        if (!IsEmpty(S)){
            T=Pop(S);//结点弹出堆栈
            printf("%5d",T->Data);//（访问）打印结点
            T=T->Right;//转向右子树
        }
    }
}
```

先序遍历的非递归遍历算法

```c
void InOrderTraversal(BinTree BT)
{
    BinTree T BT;
    Stack S = CreatStack(MaxSize);//创建初始化堆栈
    while(T||!IsEmpty(S)){
        while(T){//一直向左并将沿途结点压入堆栈
            Push(S,T);
            T=T->Left;
        }
        if(!IsEmpty(S)){
            T=Pop(S);//结点弹出堆栈
            printf("%5d",T->Data);//(访问)打印结点
            T=T->Right;//转向右子树
        }
    }
}
```

##### 层序遍历

二叉树遍历的核心问题：二维结构的线性化

- 从节点访问其左、右儿子结点
- 访问完左儿子之后，右儿子结点怎么办
    - 需要一个存储结构保存暂时不访问的结点
    - 存储结构：堆栈、队列

层序基本过程：先根结点入队，然后：

1. 从队列中取出一个元素
2. 访问该元素所指的结点
3. 若该元素所致结点的左右孩子结点非空，则将其左右孩子的指针顺序入队

```c
void LevelOrderTraversal(BinTree BT)
{
    Queue Q; BinTree T;
    if(!BQ) return ;//若是空树直接返回
    Q=CreatQueue(MaxSize);//创建并初始化队列Q
    AddQ(Q,BT);
    while(!IsEmptyQ(Q)){
        T=DeleteQ(Q);
        printf("%d\n",T->Data);//访问取出队列的结点
        if(T->Left)	AddQ(Q,T->Left);
        if(T->Right) AddQ(Q,T->Right);
    }
}
```

##### 遍历应用

【例】输出二叉树中的叶子节点

- 在二叉树的遍历算法中增加检测结点的"左右子树是否都空“

```c
void PreOrderPrintLeaves(BinTree BT)
{
    if(BT){
		if(!BT-left && !BT->Right)
    		printf("%d",BT->Data);
    	PreOrderPrintLeaves(BT->Left);
       	PreOrderPrintLeaves(BT->Right);
    }
}
```

【例】求二叉树的高度

![image-20250424215715035](images/image-20250424215715035.png)

$Height=max(H_L,H_R)+1$

```c
int PostOrderGetHeight(BinTree BT)
{
    int HL,HR,MaxH;
    if(BT){
        HL=PostOrderGetHeight(BT->Left);//求左子树的深度
        HR=PostOrderGetHeight(BT->Right);//求右子树的深度
        MaxH = (HL>HR)?HL:HR;//去左右子树较大的深度
        return (MaxH+1);//返回树的深度
    }
    else return 0;//空树深度为0
}
```

【例】二元表达式树及其遍历

![image-20250424220408437](images/image-20250424220408437.png)

表达式树

三种遍历可以得到三种不同的访问结果

- 先序遍历得到前缀表达式：++a*bc*+*defg

- 中序遍历得到中缀表达式：a+b*c+d*e+f*g

    中缀表达式会受到算数符优先集的影响

    在遍历左右子树时分别加上括号

- 后续遍历得到后缀表达式：abc*+de*f+g*+

【例】由两种遍历序列确定的二叉树

答案是必须有中序遍历才行

没有中序的困扰：

- 先序遍历序列：A B
- 后续遍历序列：B A

先序和中序遍历序列来确定一颗二叉树

【分析】

- 据先序遍历序列第一个结点确定根节点
- 根据根节点在中序遍历序列中分割除左右两个子序列
- 对左子树和右子树分别递归使用相同的方法继续分解

![image-20250424221520709](images/image-20250424221520709.png)

先序序列：a b c d e f g h i j

中序序列：c b e d a h g i j f

![image-20250424221718386](images/image-20250424221718386.png)

类似的，后序和中序遍历序列也可以确定一颗二叉树

### 例：树的同构

给定两棵树$T_1$和$T_2$，如果$T_1$可以通过若干次左右孩子互换变成$T_2$,则我们称这两颗树s是“同构的”。

现给定两颗树，请判断他们是否是同构的

输入格式：输入给出2棵树二叉树的信息

- 先在一行中给出该树的结点数，随后N行
- 第i行对应编号第i个结点，给出该结点中存储的字母、其左孩子结点的编号、右孩子结点的编号
- 如果孩子节点为空，则在相应的位置上给出“-”

求解思路

1. 二叉树表示
2. 建二叉树
3. 同构判别

二叉树表示

链表表示

![image-20250425190859890](images/image-20250425190859890.png)

数组表示

![image-20250425190815757](images/image-20250425190815757.png)

BT

| 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|      | A    | B    | C    | D    | E    | F    | G    | --   | H    | I    | --   | --   | J    |

结构数组表示二叉树：静态链表

```c
#define MaxTree 10
#define ElementType char
#define Tree int
#define NUll -1

struct TreeNode
{
    ElementType Element;
    Tree Left;
    Tree Right;
}T1[MaxTree],T2[MaxTree]
```

程序框架搭建

```c
int main(){
    
    建二叉树1;
    建二叉树2;
    判别是否同构并输出;
    
    return 0;
}
```

需要设计的函数

- 读数据建立二叉树
- 二叉树的同构判别

```c
int main ()
{
    Tree R1,R2;
    
    R1=BuildTree(T1);
    R2=BuildTree(T2);
    if(Isomorphic(R1,R2)) printf("Yes\n");
    else printf("No\n");
    
    return 0;
}
```

如何建二叉树

```c
Tree BuildTree (struct TreeNode T[])
{
    scanf("%d\n",&N);
    if(N){
        for(i=0;i<N;i++)check[i]=0;
        for(i=0;i<N;i++){
				scanf("%c %c %c\n",&T[i].Element,&cl,&cr);
        		if (c!="-"){
                    T[i].Left = cl-'0';
                    check[T[i].left]=1;
                }
        		else T[i].Left=Null;
        			/*对cr的对应处理*/
        }
    for(i=0;i<N;i++)
        if(!check[i])break;
    Root = i;
    }
    return Root;
}
```

如何判断二叉树同构

```c
int Isomorphic(Tree R1,Tree R2)
{
    if((R1==Null)&&(R2==Null))//both empty
        return 1;
    if((R1==Null)&&(R2!=Null)||(R1!=Null)&&(R2!=Null))
        return 0;//one of them is empty
    if((T1[R1].Element!=T2[R2].Element))
        return 0;//roots are different
    if((T1[R1].Left==Null)&&(T2[R2].Left==Null))
        //both have no left subtree
        return Isomorphic(T1[R1].Right,T2[R2].Right);
    if (((T1[R1].Left!=Null)&&(T2[R2].Left!=Null)&&((T1[T1[R1].left].Element)==(T2[T2[R2].Left].Element)))
        //no need to swap the left and the right
        return (Isomorphic(T1[R1].Left,T2[R2].Left) && Isomorphic(T1[R1].Right,T2[R2].Right));
}
    else//need to swap the left and the right 
        return (Isomorphic(T1[R1].Left,T2[R2].Right)&&(Isomorphic(T1[R1].Right,T2[R2].Left));
```

## 树的应用

### 二叉搜索树

查找问题：

- 静态查找与动态查找
- 动态查找，数据如何组织

二叉搜索树（BST，Binary Search Tree），也称二叉排序树或二叉查找树

二叉搜索树：一颗二叉树，可以为空；如果不为空，满足以下性质

1. 非空左子树的所有键值小于其根结点的键值
2. 非空右子树的所有键值大于其根节点的键值
3. 左、右子树都是二叉搜索树

二叉搜索树操作的特别函数：

```c
Position Find (ElementType X,BinTree BST):从二叉搜索树BST中查找元素X，返回其所在结点的地址；

Position FindMin(BinTree BST):从二叉搜索树BST中查找并返回最小元素所在结点的地址；

Position FindMax(BinTree BST):从二叉搜索树BST中查找并返回最大元素所在结点的地址；

BinTree Insert (ElementType X,BinTree BST);

BinTree Delete (ElementType X,BinTree BST);
```

#### 查找操作：Find

查找从根节点开始，如果树为空，返回NULL

若搜索树非空，则根节点关键字和X进行比较，并进行不同处理：

1. 若X小于根节点键值，只需在左子树中继续搜索；
2. 如果X大于根节点的键值，在右子树中进行继续搜索；
3. 若两者比较结果是相等，搜索完成，返回指向此结点的指针。

```c
Position Find(ElementType X,BinTree BST)
{
    if(!BST) return NULL;//查找失败
    if(X>BST->Data)
        return Find(X,BST->Right);//在右子树中继续查找
    else if (X <BST->Data)
        return Find(X,BST->left);//在左子树中继续查找
    else//X==BST->Data
        return BST;//查找成功，返回结点的找到结点的地址
}
```

都是尾递归

由于非递归函数的执行效率高，可将“尾递归”函数改为迭代函数

```c
Position IterFind (ElementType X,BinTree BST)
{
    while(BST){
        if (X>BST->Data)
            BST=BST->Right;//向右子树移动，继续查找
        else if (X<BST->Data)
            BST = BST->Left;//向左子树移动，继续查找
        else//X==BST->Data
            return BST;//查找成功，返回结点的找到结点的地址
    }
    return NULL;//查找失败
}
```

查找的效率决定于树的高度

#### 查找最大元素和最小元素

- 最大元素一定是在树的最右分枝的端结点上
- 最小元素一定是在树的最左分枝的端结点上

![image-20250425203036617](images/image-20250425203036617.png)

查找最小元素的递归函数

```c
Position FindMin(BinTree BST)
{
    if(!BST)return NULL;//空的搜索树，返回NULL
    else if (!BST->Left)
        return BST;//找到最左也结点并返回
    else 
        return FindMin(BST->Left);//沿左分支继续查找
}
```

查找最大元素的迭代函数

```c
Position FindMax(BinTree BST)
{
    if(BST)
        while (BST->Right) BST=BST->Right;
    		//沿右分支继续查找，直到最右叶结点
    return BST;
}
```

#### 插入操作：insert

关键要找到元素应该插入的位置，可以采用与Find类似方法

二叉搜索树的插入算法

```c
BinTree Insert (ElementType X,BinTree BST)
{
    if(!BST){
        //若原树为空，生成并返回一个结点的二叉搜索树
        BST=malloc(sizeof(struct TreeNode));
        BST->Data=X;
        BST->Left=BST->Right=NULL;
    }else//开始找要插入元素的位置
    {
        if(X<BST->Data)
            BST->Left = Insert(X,BST->Left);
        			//递归插入左子树
        else if (X>BST->Data)
            BST->Right=Insert(X,BST->Right);
        			//递归插入右子树
        //else X已经存在，什么都不做
        return BST
    }
}
```

例：一一年十二个月的英文缩写为键值，按从一月到十二月顺序写入及输入序列为（Jan,Feb,Mar,Apr,May,Jun,July,Aug,Sep,Oct,Nov,Dec）

![image-20250425213154538](images/image-20250425213154538.png)

### 平衡二叉树

例：搜索树结点不同插入次序，将导致不同的深度和平均查找长度ASL

![image-20250425214159809](images/image-20250425214159809.png)

(a)自然月份序列

ASL（a）=（1+2\*2+3\*3+4*3+5\*2+6\*2）=3.5

![image-20250425214851639](images/image-20250425214851639.png)

(B)按July,Feb,May,Mar,Aug,Jan,Apr,Jun.Oct,Sept,Nov,Dec

ASL(b)=3.0

![image-20250425215024880](images/image-20250425215024880.png)

（c）月份字符串大小排序

ASL（c）=6.5

“平衡因子（Balance Factor ,简称BF）:BF(T)=$h_L-h_R$

其中$h_L$和$h_R$分别为T的左、右子树的高度

平衡二叉树（Balanced Binary Tree）（AVL树）

​		空树，或者

​		任一结点左、右子树高度差不超过1集$|BF（T）|\le 1$

![image-20250425215832219](images/image-20250425215832219.png)

设$n_h$高度为h的平衡二叉树的最少结点数。结点数最少时：

![image-20250425220550188](images/image-20250425220550188.png)

斐波那契数列

$F_0=1,F_1=1,F_i=F_{i-1}+F_{i-2} for i>1$

设$n_h$时高度为h的平衡二叉树的最小结点数

![image-20250425221055231](images/image-20250425221055231.png)

$n_h=n_{h-1}+n_{h-2}+1$

$n_h=F_{h+2}-1$,对$h\ge0$

$F_i\approx\frac{1}{\sqrt{5}}(\frac{1+\sqrt{5}}{2})^i$

$n_h\approx\frac{1}{\sqrt{5}}(\frac{1+\sqrt{5}}{2})^{h+2}-1$

$h=O(log_2n)$

#### 平衡二叉树的调整

![image-20250425222255831](images/image-20250425222255831.png)

不平衡的发现者时Mar，麻烦结点Nov在发现者右子树的右边，因此叫RR插入，需要RR旋转（右单旋）

![image-20250425222454632](images/image-20250425222454632.png)

![image-20250425223149215](images/image-20250425223149215.png)

发现者时mar，麻烦结点Apr在发现者左子树的左边，因此叫LL插入，需要LL旋转（左单旋）

![image-20250425223118700](images/image-20250425223118700.png)

![image-20250425223415180](images/image-20250425223415180.png)

发现者是May，麻烦结点Jan在左子树的右边，因此叫LR插入，需要LR旋转

![image-20250425223527685](images/image-20250425223527685.png)

有时候即便不需要调整结构，也需要重新计算一些平衡因子

### 例：是否同一颗二叉搜索树

给定一颗二叉搜索树就可以唯一确定一颗二叉搜索树。然而，一颗给定的二叉搜索树却可以有多种插入序列得到

求解思路

两个序列是否对应相同搜索树判别

1. 分别建两颗搜索树的判别方法

    根据两个序列分别建树，在判别树是否一样

2. 不建树的判别法

求解思路

1. 搜索树表示
2. 建搜索树T
3. 判别一序列是否与搜索树T一致

搜索树表示

```c
typedef struct TreeNode *Tree;
struct TreeNode{
    int v;
    Tree Left,Right;
    int flag
};
```

程序框架搭建

```c
int main()
{对每组数据
    读入N和L;
    根据第一行序列建树
    根据树T分别判别后面L个序列是否能与T形成统一搜索树并输出结果
    
    return 0;
}
```

需要设计的主要函数

- 读数据建搜索树T
- 判别一序列是否与T构成一样的搜索树

```c
int main ()
{
    int N,L,i;
    Tree T;
    
    scanf("%d",&N);
    while(N){
        scanf("%d",&L);
        T=MakeTree(N);
        for(i=0;i<L;i++){
            if(Judge(T,N))printf("Yes\n");
            else printf("No\n");
            ResetT(T);//清除T中的标记flag
        }
        FreeTree(T);
        scanf("%d",&N);
    }
    return 0;
}
```

建搜索树

```c
Tree MakeTree(int N)
{
    Tree T;
    int i, V;
    
    scanf("%d",&V);
    T=NewNode(V);
    for(i=1;i<N;i++)
    {
        scanf("%d",&V);
        T=Insert(T,V);
    }
    return T;
}
```

```c
Tree NewNode(int V)
{
    Tree T=(Tree)malloc(sizeof(struct TreeNode));
    T->v=V;
    T->Left=T->Right=NULL;
    T->flag = 0;
    return T;
}
```

```c
Tree Insert(Tree T,int,V)
{
    if(!T)T=NewNode(V);
    else{
        if(V>T->v)
            T->Right = Insert(T->Right,V);
        else
            T->Left = Insert(T->Left,V);
    }
    return T;
}
```

如何判别

如何判别序列与树一致

方法：在树T中按顺序搜索序列中每个数

- 如果每次搜索所结果的结点前面均出现过，则一致
- 否则（某次搜索中遇到前面未出现的结点），则不一致

```c
int check (Tree T,int V)
{
    if(T->flag){
        if(V<t->v)return check(T->left,V);
        else if (V>T-v)check(T->Right,V);
        else return 0;
    }
    else{
        if(V==T->v){
            T->flag = 1;
            return 1;
        }
        else return 0;
    }
}
```

```c
int Judge(Tree T,int N)
{
    int i,V,flag=0;
    //flag:0代表目前还一致 flag：1代表已经不一致
    scanf("%d",&V);
    if(V!=T->v)flag=1;
    else T->flag =1;
    for(i=1;i<N;i++)
    {
        scanf("%d",&V);
        if((!flag)&&(!check(T,V)))flag=1;
    }
    if(flag)return 0;
    else return 1;
    
}
```

```c
void Reset(Tree T)//清除T中各结点的flag标记
{
    if(T->left)ResetT(T->Left);
    if(T->Right)ResetT(T->Right);
}
```

```c
void FreeTree(Tree T)//释放T的空间
{
    if(T->Left) FreeTree(T->Left);
    if(T->Right) FreeTree(T->Right);
    free(T);
}
```

## 堆，哈夫曼树，集合

### 堆

优先队列（Priority Queue）：特殊的“队列”，取出元素的顺序是依照元素的优先权（关键字）大小，而不是元素进入队列的先后顺序

若采用数组和链表实现优先队列

- 数组：

    - 插入——元素总是插入尾部					 $\varTheta(1)$

    - 删除——查找最大（或最小）关键字      $\varTheta(1)$

        ​               从数组中删去需要移动的元素  $O(n)$

- 链表：

    - 插入——元素总是插入链表的头			 $\varTheta(1)$

    - 删除——查找最大（或最小）关键字      $\varTheta(n)$

        ​               删去结点								  $\varTheta(1)$

- 有序数组：

    - 插入——找到合适的位置						 $O(n)$或$O(log_2n)$

        ​				 	 移动元素并插入				 $O(n)$

    - 删除——查找最大（或最小）关键字       $\varTheta(1)$

- 有序链表：

    - 插入——找到合适的位置						$O(n)$

        ​				插入元素					 			$\varTheta(1)$

    - 删除——删除首元素或最后元素             $\varTheta(1)$

优先队列表示的完全二叉树

![image-20250427204304923](images/image-20250427204304923.png)

|      | a    | b    | c    | d    | e    | f    | g    | h    | i    |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   |

堆的两个特性

结构性：用数组表示的完全二叉树

有序性：任一结点的关键字是其子树所有结点的最大值（或最小值）

- “最大堆（MaxHeap）”，也称“大顶堆”：最大值
- “最小堆（MinHeap） ”，也称“小顶堆”：最小值

从根节点到任意结点路径的有序性

#### 堆的抽象数据类型描述

```
类型名称：最大堆（MaxHeap）
数据对象集：完全二叉树，每个结点的元素值不小于其字节点的元素值
操作集：最大堆H∈MaxHeap，元素item∈ElementType，主要操作有：
MaxHeap Create(int MaxSize):创建一个空的最大堆
Boolean IsFull(MaxHeap H):判断最大堆H是否已满
Insert(MaxHeap H,ElementType item)；将元素item插入最大堆H
Boolean IsEmpty(MaxHeap H):判断最大堆H是否为空
ElementType DeleteMax(MaxHeap H):返回H中最大元素（高优先级）
```

#### 堆的创建

```c
typedef struct HeapStruct *MaxHeap;
struct HeapStruct{
    ElementType *Elements;//存储堆元素的数组
    int Size;//堆当前元素的个数
    int Capacity;//堆的最大容量
};
```

```c
MaxHeap Create(int MaxSize)
{
    //创建容量未MaxSize的空的最大栈
    MaxHeap H=malloc(sizeof(struct HeapStruct));
    E->Elements=malloc((MaxSize+1)*sizeof(ElementType));
    H->Size =0;
    H->Capacity = MaxSize;
    H->Elements[0]=MaxData;
    //定义“哨兵”为大于堆中所有可能元素值，便于以后更快的操作
    return H;
}
```

#### 堆的插入

算法：将新增结点插入到从其父节点到根节点的有序序列中

```c
void Insert(MaxHeap H,ElementType item)
{//将元素item插入最大堆H，其中H->Elements[0]已经定义为哨兵
    int i;
    if (IsFull(H)){
        printf("");
        return ;
    }
    i= ++H->Size;//i指向插入后堆中最后一个元素的位置
    for(;H->Elements[i/2]<item;i/=2)
        H->Elements[i]=Elements[i/2];//向下过滤结点
    H->Elements[i]=item;//将item插入
}
```

$T(N)=O(logN)$

#### 堆的删除

取出根节点（最大值）元素，同时删除堆的一个结点

```c
ElementType DeleteMax(MaxHeap H)
{//从最大堆H中取出键值最大的元素，并删除一个结点
    int Parent,Child;
    ElementType MaxItem,temp;
    if(IsEmpty(H)){
        printf("最大堆已为空");
         return;
    }
    MaxItem = H->Elements[1];//取出根节点的最大值
    //用最大堆中最后一个元素从根节点开始向上过滤下层结点
    temp=H->Elements[H->Size--];
    for(Parent=1;Parent*2<=H->Size;Parent=Child+1){
        Child = Parent*2;
        if((Child!=H->Size)&&(H->Elements[Elements[Child]<H->Elements[Child]))Child++;//Child指向左右结点的较大者
        if(temp>=H->Elements[Child])break;
      	else //移动temp元素到下一层
              H->Elements[Parent]=H->Elements[Child];
    }
    H->Elements[Parent]=temp;
    return Maxitem;                                      
}
```

#### 堆的建立

建立最大堆：将已经存在的N个元素按最大堆的要求存放在一个以为数组中

方法1：通过插入操作，将N个元素一个个相继插入到一个初始为空的堆栈中去，其时间代价最大为$O(NlogN)$

方法2：在线性时间复杂度下建立最大栈

1. 将N个元素按输入顺序存入，先满足完全二叉树的结构特性
2. 调整各结点的位置，以满足最大堆的有序特性

建堆时间复杂性：$O(n)$

树中各结点的高度和

### 哈夫曼树

【例】将百分制的考试成绩转换成五分制的成绩

```c
if(score<60)grade=1;
else if (score<70)grade=2;
else if (score<80)grade=3;
else if (score<90)grade=4;
else grade =5
```

判定树

![image-20250428190646384](images/image-20250428190646384.png)

如果考虑学生成绩分布的概率

| 分数段 | 0-59 | 60-69 | 70-79 | 80-89 | 90-100 |
| ------ | ---- | ----- | ----- | ----- | ------ |
| 比例   | 0.05 | 0.15  | 0.40  | 0.30  | 0.10   |

查找效率：0.05×10.15×2+0.4×3+0.3×4+0.1×4

修改判定数：

![image-20250428191212341](images/image-20250428191212341.png)

```c
if(score<80)
{
    if(score<70)
        if(score<60)grade=1;
    	else grade =2;
}else if(score<90)grade=4;
else grade=5;
```

效率：0.05×3+0.15×3+0.4×2+0.3×2+0.1×2=2.2

#### 哈夫曼树的定义

带权路径长度（WPL）：设二叉树有n各也子结点，每个叶子结点带有权值$w_k$,从根结点到每各子叶结点的长度为$l_k$，则每个叶子结点的带权路径长度之和就是：$WPL=\underset{k=1}{\overset{n}{\varSigma}}w_kl_k$

最优二叉树或哈夫曼树：WPL最小二叉树

#### 哈夫曼树的构造

每次把权值最小的两棵二叉树合并

```c
typedef struct TreeNode *HuffmanTree;
struct TreeNode{
    int Weight;
    HuffmanTree Left,Right;
}
HuffmanTree Huffman(MinHeap H)
{//假设H->Size个权值已经存在H->Elements[]->Weight里
    int i;HuffmanTree T;
    BuildMinHeap(H);//将H->Elements[]按权值调整为最小堆
    for(i=1;i<h->Size;i++){//做H->Size-1次合并
        T=malloc(sizeof(struct TreeNode));//建立新结点
        T->Left = DeleteMin(H);
        			//从最小堆中删除一个结点，作为新T的左子结点
        T->Right = DeleteMin(H);
        			//从最小堆中删除一个结点，作为新T的右子结点
        T->Weight = T->Left->Weight+T->Right->Weight;
        			//计算新权值
        Insert(H,T);//将T插入最小堆
    }
    T=DeleteMin(H);
    return T;
}
```

整体复杂度为$O(NlogN)$

哈夫曼树的特点：

- 没有度为1的点
- n个叶子节点的哈夫曼树共有2n-1个结点
- 哈夫曼树的任意非叶节点的左右子树交换后仍是哈夫曼树
- 对于同一组权值可能存在不同构的哈夫曼树

#### 哈夫曼编码

给定一段字符串，如何堆字符进行编码，可以使得该字符串的编码存储空间最少

【例】假设有一段文本，包含58个字符，并由以下7个字符构成：a，e，i，s，t，空格（sp），换行（nl）；者七个字符出现的次数不同。如何堆7个字符进行编码，使得总编码空间最少

【分析】

1. 用等长ASCII编码：58×8=464位
2. 用等长3位编码：58×3=174位
3. 不等长编码：出现频率高的字符用的编码短些，出些频率第的字符可以编码长些

如何避免二义性：

前缀码prbefix code :任何字符的编码都不是另一字符编码的前缀

- 可以无二义地编码

二叉树用于编码：

1. 左右分支：0、1
2. 字符只在叶节点上

四个字符频率：a：4，u：1，x：2，z：1

![image-20250428200951131](images/image-20250428200951131.png)

Cost(aaaxuzxz -> 0000001001001011)=2×4+2×1+2×2+2×1=16

![image-20250428201142514](images/image-20250428201142514.png)

Cost(aaaxuzxz -> 0000001001001011)=1×4+3×1+2×2+3×1=14

【例】哈夫曼编码

| $C_i$ | a    | e    | i    | s    | t    | sp   | nl   |
| ----- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| $f_i$ | 10   | 15   | 12   | 3    | 4    | 13   | 1    |

- a:111
- e:10
- i:00
- s:11011
- t:1100
- sp:01
- nl:11010

![image-20250428201645288](images/image-20250428201645288.png)

Cost=3×10+2×15+2×12+5×3+4×4+2×13+5×1=146

### 集合

集合运算：交，并，补，差，判定一个元素是否属于某一集合

并差集：集合并，差某元素属于什么集合

并查集问题中集合存储入和实现？

可以用树结构表示集合，树的每个结点代表结合元素

例如，有三个整数集合

S1={1,2,4,7}

S2={3,5,8}

S3={6,9,10}

![image-20250428203124837](images/image-20250428203124837.png)

 双亲表示法：孩子指向双亲

采用数组存储形式

| 下标   | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |
| ------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Data   | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   |
| Parent | -1   | 0    | -1   | 0    | 2    | -1   | 0    | 2    | 5    | 5    |

#### 数组中每个元素的类型描述为：

```c
typedef struct{
    ElemenType Data;
    int Parent;
}SetType
```

#### 集合运算

1. 查找某个元素所在的集合（用根节点表示）

    ```c
    int Find(SetType S[],ElementType X)
    {	//在数组S中查找只为X的元素所属的集合
        //MaxSize是全局变量，为数组S的最大长度
        int i;
        for(i=0;i<MaxSize&&S[i].Data!=X;i++);
        if(i>=MaxSize)return -1;//未找到X，返回-1
        for(;S[i].Parent>=0;i=S[i].Parent);
        return i;//找到X所属集合，返回树根所在结点在数组S中的下标
    }
    ```

2. 集合的并运算

    1. 分别找到X1和X2两个元素所在集合树的根节点
    2. 如果他们不同根，则将其中一个根节点的父结点指针设置成另一个根节点的数组下标

    ```c
    void Union(SetType S[],ElementType X1,ElementType X2)
    {
        int Root1,Root2;
        Root1 = Find(S,X1);
        Root2 = Find(S,X2);
        if(Root1!=Root2)S[Root2].Parent=Root1;
    }
    ```

    为了改善合并以后的查找性能，可以采用小的集合合并到相对大的集合中修改Union函数

### 例：File Transfer

#### 集合的简化表示

```c
typedef struct {
    ElementType Data;
    int Parent;
}SetType;

int Find(SetType s[],ElementType X)
{
    int i;
    for(i=0;i<MaxSize && S[i].Data!=X;i++)
    if(i>=MaxSize) return -1;
    for(;S[i].Parent>=0;i=S[i].Parent);
    return i;
}
```

任何有限集合的（N个）元素都可以被意义映射为整数0~N-1

| 下标 | [0]  | [1]  | [2]  | [3]  | [4]  | [5]  | [6]  |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| S    | 6    | 6    | -1   | 4    | 2    | 2    | -1   |

```c
typedef int ElementType;//默认元素可以用非负整数表示
typedef int SetName;//默认用根节点表示下标作为集合名称
typedef ElementType SetType[MaxSize];

SetName Find(SetType S,ElementType X)
{//莫仍集合元素全部初始化为-1
    for(;S[X]>=0;X=S[X]);
    return X;
}

void Union(SetType S,SetName Root1,SetName Root2)
{//这里默认Root1和Root2是不同集合的根节点
    S[Root2]=Root1
}
```

#### 程序框架搭建

```c
int main()
{
    初始化集合;
    do{
        读入一条指令;
        处理指令;
    }while(没结束);
    return 0;
}
```

```c
int main()
{
    SetType S;
    int n;
    char in;
    scanf("%d\n",&n);
    Initialization(S,n);
    do{
        scanf("%c",&in);
        switch (in){
            case "I":Input_connection(S);break;
            case "C":Check_connection(S);break;
            case "S":Check_network(S);break;
        }
    }while(in!='S');
    return 0;
}
```

```c
void input_connection(SetType S)
{
    ElementType u,v;
    SetName Root1,Root2;
    scanf("%d %d\n",&u,&v);
    Root1=Find(S,u-1);
    Root2=Find(S,v-1);
    if(Root1!=Root2)
        Union(S,Root1,Root2);
}

void Check_connection(SetType S)
{
    ElementType u,v;
    SetName Root1,Root2;
    scanf("%d %d\n",&u,&v);
    Root1=Find(S,u-1);
    Root2=Find(S,v-1);
    if(Root1==Root2)
  		printf("yes\n");
    else printf("no\n");
}

void Check_network(SetType S,int n)
{
    int i,counter=0;
    for(i=0;i<n;i++){
        if(S[i]<0) counter++;
    }
    if(counter==1)
        printf("The network is connected.\n");
    else
        printf("There are %d components.\n",counter)
}
```

#### 按秩归并

为什么需要按秩归并

$T(n)=O(n^2)$

树会越来越高

将矮树贴到高树上

存储树的高度

S[Root]=-树高

任然初始化为-1

```c
if(Root2高度>Root1高度)
    S[Root1]=Root2;
else {
    if(两者等高)树高++;
    S[Root2]=Root1;
}
```

```c
if(S[Root2]<S[Root1])
    S[Root1]=Root2;
else {
    if(S[Root1]==S[Root2])S[Root1]--;
    S[Root2]=Root1;
}
```

另一种做法：比规模

- 把小树贴到大树上	S[Root]=-元素个数;

    ```c
    void Union(SetType S,SetName Root1，SetName Root2)
    {
    	if(S[Root2]<S[Root1]){
            S[Root2]+=S[Root1];
        	S[Root1]=Root2;
        }
        else {
        	S[Root1]+=S[Root2]
        	S[Root2]=Root1;
    }
    ```

两者方法统称“按秩归并”

最坏的情况的树高=$O(logN)$

#### 路径压缩

```c
SetName(SetType S,ElementType X)
{
    if (S[X]<0)//找到集合的根
        return X;
    else
        return S[X] = Find(S,S[X]);
}
```

先找到根，把根变成X的父节点；在返回根。

#### 时间复杂度

【引理（Tarjan）】令$T(M,N)$为交错执行$M\ge N$次带路径压缩的查找和$N-1$次按秩归并的最坏情况时间。则存在正常数$k_1$和$k_2$，使得：

$k_1M\alpha(M,N)\le T(M,N)\le k_2M\alpha(M,N)$

Ackermann函数和$\alpha (M,N)$

$A(i,j)\begin{cases}2^j\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,i=1\,\,and\,\,  j\ge1\\A(i-1,2)\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,i\ge2 \,\,and\,\,j=1\\A(i-1,A(i,j-1))\,\,\,\,\,\,i\ge2\,\,and\,\,j\ge2\end{cases}$

$\alpha(M,N)=min\{{i\ge 1|A(i,[M/N])>logN}\}\le O(log^*N)\le 4$

$log^*N$(Ackermann反函数)=堆N求对数知道结果$\le$1的次数

### 例：堆中的路径

将一系列给定的数字插入一个初始为空的小顶堆H[]。随后对任意给定下标‘i’，打印从H[i]到根节点的路径

堆的表示及其操作

```c
#define MAXN 1001
#define MINH -10001

int H[MAXH],size;

void Create()
{
    size = 0;
    H[0]=MINH;
    //设置岗哨
}

void Insert(int X)
{
    //将X插入H。这里省略检查堆是否已满的代码
    int i;
    
    for(i=++size;H[i/2]>X;i/=2)
        H[i]=H[i/2];
    H[i]=X;
}
```

主程序

```c
int main()
{
    读入n和m;
    根据输入序列建堆;
    对m个要求：打印到根的路径;    
    return 0;
}
```

```c
int main()
{
    int n,m,x,i,j;
    
    scanf("%d %d",&n,&m);
    Create();//
    for(i=0;i<n;i++){//
        scanf("%d",&x);
        Insert(x);
    }
    for(i=0;i<m;i++){
        scanf("%d",&j);
        printf("%d",H[j]);
        while(j>2){//
            j/=2;
            printf("%d",H[j]);
        }
        printf("\n");
    }
    return 0;
}
```

### 例：Tree Traversals Again

非递归中序遍历

- Push的顺序为先序遍历
- Pop的顺序给出中序遍历

核心算法

![image-20250429205456230](images/image-20250429205456230.png)

```c
void solve(int prel, int inL,int postL, int n)
{
    if(n==0) return ;
    if(n==1) { post[postL]=pre[preL];return;}
	root =pre[preL];
    post[PostL+n-1]=root;
    for(i=0;i<n;i++)
        if(in[inL+i]==root) break;
    L = i; R= n-L-1;
    solve(preL+1,intL,postL,L);
    solve(preL+L+1,inL+L+1,postL+L,R);
    
    }
}
```

### 例：cpmplete Binary Search Tree（完全二叉搜索树)

​					二叉搜索树												完全二叉树

![image-20250429211508587](images/image-20250429211508587.png)

树的表示法：链表vs.数组

需要操作：

- 填写数字（某种遍历）
- 层序遍历



- 完全二叉树，不浪费空间
- 层序遍历==直接顺序输出

核心算法

![image-20250429213431956](images/image-20250429213431956.png)

```c
void solve(int ALeft,int ARight,int TRoot)
{//初始调用为solve (0,N-1,0)
    n=ARight -Aleft +1;
    if(n==0) return ;
    L=GetLeftLength(n);//计算出n个结点的树其左子树有多少个结点
    T[TRoot]=A[ALeft+L];
    LeftTRoot =TRoot*2+1;
    RightTRoot = LeftTRoot +1;
    solve(ALeft,ALeft+L-1,LeftTRoot);
    solve(ALeft+L+1,ARight,RightTRoot);
}
```

排序

```c
#include <stdlib.h>
int compare(const void*a,const void*b)
{
    return *(int*)a-*(int*)b;
}

int main()
{
	qsort(A,N,sizeof(int),compare);
}
```

计算左子树规模

![image-20250429215517188](images/image-20250429215517188.png)

$H=[log_2(N+1)]$

最小$X=0$

最大$X=2^{H-1}$

$X=min{X,2^{H-1}}$

$L=2^{H-1}-1+X$

### 例：哈夫曼编码

huffmancode的特点

1. 最优编码——总长度（WPL）最小
2. 我歧义解码——前缀码：数据仅存于叶子结点
3. 没有度为1的结点——满足1、2必有3

核心算法：

1. 计算最优编码长度

    ```c
    MinHeap H = CreateHeap(N);//创建一个空的、容量为N的最小堆
    H=ReadData(N);//将f[]读入H->Data[]中
    HuffmanTree T= Huffman(H);//建立Huffman树
    int Codelen = WPL(T,0);
    ```

    ```c
    int WPL (HuffmanTree T,int Depth)
    {
        if(!T->Left&&!T->Right)
            return (Depth*T->weight);
        else //否则T一定有2个孩子
            return (WPL(T->Left,Depth+1)+WPL(T->Right,Depth+1));
    }
    ```

2. 对每位学生的提交、检查

    1. 长度是否正确，检查

        $Len=\underset{i=0}{\overset{N-1}{\varSigma}}strlen(code[i])\times f[i]$

        注意：Code[i]的最大长度为N-1

        ![image-20250504200856016](images/image-20250504200856016.png)

    2. 建树的过程中检查是否满足前缀码要求

        Code[i]="1011"

        Code[i]="100"

        Code[i]="1001"错

        Code[i]="101"错

        ![image-20250504200914274](images/image-20250504200914274.png)

## 图

### 图

六度空间理论(Six Degrees of Sepraration)

表示一种多对多关系

包含：

- 一组顶点：通常用V（Vertex）表示顶点的集合

- 一组边：通常用E（Edge）表示边的集合

    - 边是顶点对：（v,w）∈E，其中v,w∈V

    - 有向边<v,w>表示从v指向w的边（单行线）

        ![image-20250504202559655](images/image-20250504202559655.png)

    - 不考虑重边和自回路

        ![image-20250504202650017](images/image-20250504202650017.png)

#### 抽象数据类型

```
类型名称：图（Graph）
数据对象集：G(V,E)由一个非空的有限顶点的集合V和一个有限边的集合E组成
操作集：对于任意图G∈Graph，以及v∈V，e∈E
Graph Create():建立并返回空图；
Graph InsertVertex(Graph G,Vertex v):将v插入G；
Graph InsertEdge(Graph G,Edge e):将e插入G；
void DFS(Graph G,Vertex v):从顶点v出发深度优先遍历图G；
void BFS(Graph G,Vertex v):从顶点v出发宽度优先遍历图G；
void ShortestPath(Graph G,Vertex v,int Dist[]):计算图G中顶点v到任意其他顶点的最短距离；
void MST(Graph G):计算图G的最小生成树
```

#### 图的表示——邻接矩阵表示法

邻接矩阵G[N]\[N]——N个顶点从0到N-1个编号

$G[i][j]\begin{cases}0\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,若<v_i,v_j>是G中的边\\{1}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,否则\end{cases}$

问题：对于无向图的存储，怎样可以节省一半的空间

![image-20250504212349505](images/image-20250504212349505.png)

用一个长度为(N+1)N/2的一维数组A存储

$\{G_{00},G_{10},G{11}……,G_{n-1\, 0},……,G_{n-1\,n-1}\}$

则$G_{ij}$在A中对应的下标是：

（i*（i+1)/2+j)

对于网络，只要把G[i]\[j]的值定义为边<$v_i$，$v_j$>的权重即可

好处：

只观、简单、方便理解

方便检查任意一对顶点是否存在边

方便找任一顶点所有的"连接点"（有边直接相连的顶点）

方便计算任一顶点的“度”（从该点出发的边数为"出度"，指向该点的边数为"入度")

- 无向图：对应行(或列)非0元素的个数
- 有向图：对应行非零元素的个数是“出度”；对应列非0元素的个数是“入度”

缺点：

浪费空间——存稀疏图（点很多而变很少）有大量无效的元素

- 稠密图（特别是完全图还是很划算的）

浪费时间——统计系数图中一共有多少边

#### 图的表示——邻接表表示法

邻接表：G[N]为指针数组，对应的矩阵每行一个链表，只存非0元素

![image-20250504214754295](images/image-20250504214754295.png)

一定要够稀疏才合算

邻接表：

方便找任一顶点的所有”邻接点“

节约系数图的空间

需要N个头指针+2E个结点（每个结点至少2个域）

方便计算任一结点的度

对无向图：是的

对有向图：只能计算出度。需要构造”逆邻接表“（指存向自己的边）来方便计算"入度"

方便检查任意一对顶点间是否存在边

#### 图的遍历——DFS

深度优先搜索（Depth First Search ,DFS）

```c
void DFS (Vertex V)
{
    visited[V] = true;
    for(V的每一个邻接点W)
        if(!visited[W])
            DFS(W);
}
```

若有N个顶点、E条边、时间复杂度是

- 用邻接表存储图，有$O(N+E)$
- 用邻接矩阵存储图，有$O(N^2)$

#### 图的遍历——BFS

广度优先搜索（Breath First Search ，BFS）

![image-20250505203112818](images/image-20250505203112818.png)



```c
void BFS(Vertex V)
{
    visited[V] = true;
    Enqueue(V,Q);
    while(!IsEmpty(Q)){
        V=Dequeue(Q);
        for(V 的每个邻接点 W)
            if (!visited[W]){
                visited[W] = true;
                Enqueue(W,Q);
            }
    }
}
```

若有N个顶点、E条边、时间复杂度是

- 用邻接表存储图，有$O(N+E)$
- 用邻接矩阵存储图，有$O(N^2)$

#### 图不连通怎么办

- 连通：如果从V到W存在一条（无向）路径，则称V和W是连通的

- 路径：V和W的路径是一系列顶点$\{V,V_1,V_2,...,V_n,W\}$的集合，其中任一对相邻顶点间都有图的边。路径的长度是路径中的边数（如果带权，则是所有边的权重和）。如果V到W之间的所有顶点都不同，则称简单路径

- 回路：起点等于终点的路径

- 连通分量：无向图的极大连通子图

    - 极大顶点数：在加一个顶点就不通了

    - 极大边数：包含子图中所有顶点相连的所有边

        ![image-20250505205704862](images/image-20250505205704862.png)

- 强连通：有向图中顶点v和w之间存在双向路径，则称V和W是强连通的

- 强连通图：有向图中任意量顶点均强连通

- 强连通分量：有向图的极大强连通子图

    ![image-20250505205952671](images/image-20250505205952671.png)

```c
void DFS(Vertex V)
{
    visited[V]=true;
    for(V的每个邻接点W)
        if(!visited[W])
            DFS(W);
}
```

每调用一次DFS(V),就把V所在的连通分量遍历了一遍。BFS也一样。

```c
void ListComponents(Graph G)
{
    for(each V in G)
        if(!visited[V]){
            DFS(V);//BFS(V)
        }
}
```

### 图的应用

#### 例：拯救007

![image-20250505210918537](images/image-20250505210918537.png)

```c
void save007(Graph G)
{
    for(each V in G){
        if(!visited[V] && FirstJump(V)){
            answer = DFS(V);
            if(answer ==YES) break;
        }
    }
    if (answer==YES) output("Yes");
    else output("No");
}
```

```c
int DFS(Vertex V)
{
    visited[V]=true;
    if(IsSafe(V))answer = YES;
    else{
        for(each W in G)
            if(!visited[W] && Jump(V,W)){
                answer = DFS(W);
                if(answer == YES) break;
            }
    }
    return answer;
}
```

#### 例：六度空间(Six Degrees of Separation)

你和任何一个陌生人之间所间隔的人不超过6个

给定社交网络图，请对每个节点计算符合"六度空间"理论的结点占结点总数的百分比

算法思路：

- 对于每个节点，进行广度优先搜索

- 搜索过程中累计访问的结点数

- 需要记录“层”数，仅计算6层以内的节点数

    ```c
    void SDS()
    {
        for(each V in G){
            count = BFS(V);
            Output(count/N);
        }
    }
    ```

    ```c
    int BFS ( Vertex V)
    {
        visited[V]=true;count=1;
        Enqueue(V,Q);
        while(!IsEmpty(Q)){
            V=Dequeue(Q);
            for(V的每个邻接点W)
                if(!visited[W]){
                    visited[W]=true;
                    Enqueue(W,Q);count++;
                }
            if(V==last){
                level++;last=tail;
            }
            if(level==6)break; 
        }
        return count;
    }
    ```


#### 例：图的表示

##### 用邻接矩阵表示图

$G[i][j]\begin{cases}0\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,若<v_i,v_j>是G中的边\\{1}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,否则\end{cases}$

```c
typedef struct GNode *PtrToGNode;
struct GNode {
    int Nv;//定点数
    int Ne;//边数
    WeightType G[MaxVertexNum] [MaxVertexNum];
    DataType Data[MaxVertexNum];//存顶点的数据
};
typedef PtrToGNode MGraph;//以邻接矩阵存储图的类型
```

###### MGraph的初始化

初始化一个有VertexNum个顶点但没有边的图

```c
typedef int Vertex//用顶点下标表示顶点,表示整型
MGraph CreateGraph(int VertexNum)
{	
    Vertex V,W;
    MGraph Graph;
    
    Graph =(MGraph)malloc(sizeof(struct GNode));
    Graph->Nv= VertexNum;
    Graph->Ne= VertexNum;
    
    //注意：这里默认顶点编号从0开始，到(Graph->Nv-1)
    for(V=0;V<Graph->Nv;V++)
        for(W=0;W<Graph->Nv;W++)
            Graph->G[V][W]=0;//或INFINITY
    
    return Graph;
}
```

###### 向MGraph中插入边

```c
typedef struct ENode *PtrToENode;
struct ENode{
    Vertex V1,V2;//有向边<V1,V2>
    WeightType Weight;//权重
};
typedef PtrToENode Edge;

void InsertEdge(MGraph Graph,Edge E)
{
    //插入边<V1，V2>
    Graph->G[E->V1][E->V2] = E->Weight;
    
    //若是无向图，还要插入边<V2，V1>
    Graph->G[E->V2][E->V1] = E->Weight;
}
```

###### 完整建立一个图

输入格式

Nv Ne

V1 V2 Weight

```c
MGraph BuildGraph()
{
    MGraph Graph;
    Edge E;
    Vertex V;
    int Nv,i;
    
    scanf("%d",&Nv);
    Graph = CreateGraph(Nv);
    scanf("%d",&(Graph->Ne));
    if(Graph->Ne!=0){
        E=(Edge)malloc(sizeof(struct ENode));
        for(i=0;i<Graph->Ne;i++){
            scanf("%d %d %d",
                 &E->V1,&E->V2,&E->Weight);
            InsertEdge(Graph,E);
        }
    }
    //如果顶点有数据的话，读入数据
    for(V=0;V<Graph->Nv;V++)
        scanf("%c",&(Graph->Data[V]));
    
    return Graph;
}
```

简单方法

```c
int G[MAXN][MAXN],Nv,Ne;
void BuildGraph()
{
    int i,j,v1,v2,w;
    
    scanf("%d",&Nv);
    //CreateGraph
    for(i=0;i<Nv;i++)
        for(j=0;J<Nv;j++)
            G[i][j]=0;//或INFINITY
    scanf("%d",&Ne);
    for(i=0;i<Ne;i++)
    {
        scanf("%d %d %d",&v1,&v2,&w);
        //InsertEdge
        G[V1][V2]=w;
        G[V2][V1]=w;
    }
}
```

##### 用邻接表表示图

邻接表：G[N]为指针数组，对应矩阵每行一个链表之村非零元素

```c
typedef struct GNode *PtrToGNode;
struct GNode{
    int Nv;//顶点数
    int Ne;//边数
    AdjList G;//邻接表
};
typedef PtrToGNode LGraph;
//以邻接表方式存储数据

typedef struct Vnode{
    PtrToAdjVNode FirstEdge;
    DataType Data;//存顶点的数据
}AdjList[MaxVertexNum];
//AdjList是邻接表类型

typedef struct AdjVNode *PtrToAdjVNode;
struct AdjVNode {
    Vertex AdjV;//邻接点下注
    WeightType Weight;//边权重
    PtrToAdjVNode Next;
}
```

LGraph

初始化一个有VertexNum个顶点但没有边的图

```c
typedef int Vertex;//
LGraph CreateGraph(int VertexNum)
{
    Vertex V,W;
    LGraph Graph;
    
    Graph =(LGraph)malloc(sizeof(struct GNode));
    Graph->Nv=VertexNum;
    Graph->Ne=0;
    
    //
    for(V=0;V<Graph->Nv;V++)
        Graph->G[V].FirstEdge=NULL;
    
    return Graph;
}
```

向LGraph中插入边

```c
void InsertEdge(LGraph Graph,Edge E)
{
    PtrToAdjVNode NewNode;
    //插入边<v1,v2>
    //为V2建立新的邻接点
    NewNode=(PtrToAdjVNode)malloc(sizeof(struct AdjVNode));
    NewNode->AdjV= E->V2;
    NewNode->Weight=E->Weight;
    //将V2插入V1的表头
    NewNode->Next=Graph->G[E->V1].FirstEdge;
    Graph->G[E->V1].FirstEdge = NewNode;
    
    //无向图，还要插入边<V2,V1>
    //为V1建立新的邻接点
    NewNode=(PtrToAdjVNode)malloc(sizeof(struct AdjVNode));
    NewNode->AdjV= E->V1;
    NewNode->Weight=E->Weight;
    //将V1插入V2表头
    NewNode->Next=Graph->G[E->V2].FirstEdge;
    Graph->G[E->V2].FirstEdge = NewNode;
}
```

## 图的最短路径问题

在网络中，求两个不同顶点之间所有路径中，边的权值之和最小的那一条路径

- 这条路径就是两点之间的最短路径(Shortest Path)
- 第一个顶点为源点(Source)
- 在最后一个顶点为终点(Destination)

单源最短路径问题：从某固定源点出发，求其到所有其他顶点的最短路径

- （有向）无权图
- （有向）有权图

多源最短路径问题：任意两顶点间的最短路径

### 无权图的单源最短路算法

- 按照递增（非递减）的顺序找出各个顶点的最短路

```c
void Unweighted (Vertex S)
{
    Enqueue(S,Q);
    while(!IsEmpty(Q)){
        V=Dequeue(Q);
        for(V的每个邻接点W)
            if(dist[W]==-1){
                dist[W]=dist[V]+1;
                path[W]=V;
                Enqueue(W,Q);
            }
    }
}
```

$T=O(|V|+|E|)$

dist[W]=S到W的最短距离

dist[S]=0

path[W]=S到W的路上经过某顶点

### 有权图的单元最短路算法

![image-20250507210333791](images/image-20250507210333791.png)

- 按照递增的顺序找出到各个顶点的最短路

Dijkstra算法

- 令S={源点s+已经确定了最短路径的顶点$V_i$}
- 对任一未收录的顶点v，定义dist[v]为s到v的最短路径长度，但该路径仅经过S中的顶点。即路径$\{s→(v_i∈S)→v\}$的最小长度
- 若路径是按照递增（非递减）的顺序生成的，则
    - 真正的最短路必须只经过S中的顶点
    - 每次从未收录的顶点中选一个dist最小的收录（贪心）
    - 每增加一个v进入S，可能影响另一个w的dist值
        - dist[w]=min{dist[w],dist[v]+<v,w>的权重}

```c
void Dijkstra(Vertex s)
{
    while(1){
        V=未收录顶点中dist最小者;
        if(这样的V不存在)
            break;
        collected[V]=true;
        for(V的每个邻接点W)
            if(collected[W]==false)
                if(dist[V]+E<v,w><dist[W]){
                    dist[W]=dist[V]+E<v,w>;
                    path[W]=V;
                }
    }
}//不能解决有负边的情况
```

方法1：直接扫描所有未收录顶点$-O(|V|)$

- $T=O(|V^2|+|E|)$
- 对于稠密图效果好

方法2：将dist存在最小堆中$-O(log|V|)$

- 更新dist[w]的值 $-O(log|V|)$
- $T=O(|V|log|V|+|E|log|V|)=O(|E|log|V|)$
- 对于稀疏图效果好

### 多源最短路算法

- 方法1：直接将单源最短路算法调用|V|遍
    - $T=O(|V|^3+|E|\times |V|)$
    - 对稀疏图的效果好
- 方法2：Floyd算法
    - $T=O(|V|^3)$
    - 对稠密图效果好

Floyd算法

- $D^k[i][j]$=路径$\{i\rightarrow\{l\le k\}\rightarrow j\}$的最小长度
- $D^0,D^1,...,D^{|V|-1}[i][j]$即给出了i到j的真正最短距离
- $D^{-1}$是初始化矩阵就是邻接矩阵
- 当$D^{k-1}$已经完成，递推到$D^k$时：
    - 或者$k\notin$最短路径$\{i\rightarrow\{l\le k\}\rightarrow j\}$，则$D^k=D^{k-1}$
    - 或者k$\in$最短路径$\{i\rightarrow\{l\le k\}\rightarrow j\}$，则该路径必定有两段最短路径组成：$D^k[i][j]=D^{k-1}[i][k]+D^{k-1}[k][j]$

```c
void Floyd()
{
    for (i=0;i<N;i++)
        for(j=0;j<N;j++){
            D[i][j]=G[i][j];
        }
    for(k=0;k<N;k++)
		for(i=0;i<N;i++)
            for(j=0;j<N;j++)
                if(D[i][k]+D[k][j]<D[i][j]){
                    D[i][j]=D[i][k]+D[k][j];
                    Path[i][j]=k;
                }
}
```

### 例：哈利波特的考试

![image-20250508210609675](images/image-20250508210609675.png)

#### 程序框架搭建

```c
int main()
{
    读入图;
    分析图;
    return 0;
}
```

```c
int main()
{
    MGraph G = BuildGraph();
    FindAnimal(G);
    return 0;
}
```

![image-20250508211035567](images/image-20250508211035567.png)

#### 选择动物

```c
void FindAnimal(MGraph Graph)
{
    WeightType D[MaxVertexNum][MaxVertexNum],MaxDist,MinDist;
    Vertex Animal,i;
    
    Floyd (Graph,D);
    
    MinDist = INFINITY;
    for(i=0;i<Graph->Nv;i++){
        MaxDist=FindMaxDist(D,i,Graph->N);
        if(MaxDist==INFINITY)//说明有从i无法变出的动物
        {
            printf("0\n");
            return;
        }
        if (MinDist>MaxDist){//找出最长距离更小的动物
            MinDist = MaxDist;
            Animal = i+1;//更新距离，记录编号
        }
    }
    printf("%d %d\n",Animal,MinDist);
}
```

```c
WeightType FindMaxDist(WeightType D[][MaxVertexNum],Vertex i,int N)
{
    WeightType MaxDist;
    Vertex j;
    
    MaxDist=0;
    for(j=0;j<N;j++)//找出i到其他动物j的最长距离
        if(i!=j &&D[i][j]>MaxDist)
            MaxDist=D[i][j];
    return MaxDist
}
```

#### 模块的引用与裁剪

```c
#define MaxVertexNum 100//最大顶点数设为100
#define INFINITY 65535//设为双字节无符号整数的最大值65535
typedef int Vertex;//用顶点下标表示顶点，为整型
typedef int WeightType;//边的权值设为整型
//typedef char DataType; 顶点存储的数据类型为字符型

//边的定义
typedef struct ENode *PtrToENode;
struct ENode{
    Vertex V1,V2;//有向边<V1,V2>
    WeightType Weight;//权重
};
typedef PtrToENode Edge;

//图结点的定义
typedef struct GNode *PtrToGNode;
struct GNode{
    int Nv;//顶点数
    int Ne;//边数
    WeightType G[MaxVertexNum][MaxVertexNum];//邻接矩阵
    //DataType Data[MaxVertexNum] 存顶点的数据
    //注意很多情况下，顶点无数据，此时Data[]可以不用出现
};
typedef PtrToGNode MGraph;//以邻接矩阵存储图的类型、

MGraph CreateGraph(int VertexNum)
{//初始化一个有VertexNum个顶点但没有边的图
    Vertex V,W;
    MGraph Graph;
    
    Graph=(MGraph)malloc(sizeof(struct GNode));//建立图
    Graph->Nv=VertexNum;
    Graph->Ne=0;
    //初始化邻接矩阵
    //注意这里默认顶点编号从0开始，到(Graph->Nv-1)
    for(V=0;V<Graph->Nv;V++)
        for(W=0;W<Graph->Nv;W++)
            Graph->G[V][W]=INFINITY;
    
    return Graph;
}

void InsertEdge(MGraph Graph,Edge E)
{
    //插入边<v1,v2>
    Graph->G[E->V1][E->V2]=E->Weight;
    //若是无向图，还要插入边<v2,v1>
    Graph->G[E->V2][E->V1]=E->Weight;
}

MGraph BuildGraph()
{
    MGraph Graph;
    Edge E;
    //Vertex V;
    int Nv,i;
    scanf("%d",&Nv);//读入顶点的个数
    Graph=CreateGraph(Nv);//初始化有Nv个顶点但是没有边的图
    
    scanf("%d",&(Graph->Ne));//读入边数
    if(Graph->Ne!=0){//如果有边
        E=(Edge)malloc(sizeof(struct ENode));//建立边接点
        //读入边，格式为“起点 终点 权重”插入邻接矩阵
        for(i=0;i<Graph->Ne;i++){
			scanf("%d %d %d",&E->V1,&E->V2,&E->Weight);
        	E->V1--;E->V2--;//起始编号从0开始
        	InsertEdge(Graph,E);
        }
    }
    //如果顶点有数据的话，读入数据
    //for(V=0;V<Graph->Nv;V++)
    	//scanf(" %c",&(Graph->Data[V]));
    return Graph
}

/*bool*/void  Floyd(MGraph Graph ,WeightType D[][MaxVertexNum],/*Vertex path[][MaxVertexNum]*/)
{
    Vertex i,j,k;
    //初始化
    for (i=0;i<Graph->Nv;i++)
        for(j=0;j<Graph->Nv;j++){
            D[i][j]=Graph->G[i][j];
            //Path [i][j]=1;
        }
    for(k=0;k<Graph->Nv;k++)
		for(i=0;j<Graph->Nv;i++)
            for(j=0;j<Graph->Nv;j++)
                if(D[i][k]+D[k][j]<D[i][j]){
                    D[i][j]=D[i][k]+D[k][j];
                    Path[i][j]=k;
                    //if(i==j && D[i][j]<0)//若发现负值圈
                    	//return false; //不能正确解决，返回错误标记
                    //path[i][j]=k;
                }
		//return true;//算法执行完毕，返回正确标记
}
```

## 图的最小生成树问题

### 最小生成树

是一颗树

- 无回路
- |V|个顶点一定有|V|-1条边

是生成树

- 包含全部顶点
- |V|-1条边都在图里

边的权重和最小

向生成树中任加一条边都一定构成回路

最小生成树存在$\leftrightarrow$图连通

![image-20250510173607547](images/image-20250510173607547.png)

### 贪心算法

贪：每一步都要最好的

好：权重最小的两条边

需要约束：

- 只能用图里有的边
- 只能正好用掉|V|-1条边
- 不能有回路

### Prim算法——让小树长大

![image-20250510180034128](images/image-20250510180034128.png)

![image-20250510180401683](images/image-20250510180401683.png)

```c
void Prim()
{
    MST={s};
    while(1){
        V=未收录顶点中dist最小者
        if(这样的V不存在)
            break;
        将V收录仅MST：dist[V]=0;
        for(V的每个邻接点W)
            if(dist[W]!=0)
                if(E(v,w)<dist[W]){
                    dist[W]=E(v,w);
                    parent[W]=V;
                }
            
    }
    if(MST中收的顶点不到|V|个)
        Error ("生成树不存在");
}
```

dist[V]=E(s,V)或正无穷

parent[s]=-1

$T=O(|V|^2)$	稠密图合算

### Kruskal算法——将森林合并成树

```c
void Kruskal(Graph G)
{
    MST={};
    while(MST中不到|V|-1条边 && E中还有边 ){
        从E中取一条权重最小的边E(v,w);//最小堆
        从E(v,w)从E中删除;
        if(E(v,w)不在MST中构成回路)//并查集
            将E(v,w)加入MST;
        else
            彻底无视E(v,w);
    }
    if(MST中不到|V|-1条边)
        Erroe("生成树不存在");
            
    }
}
```

$T=O(|E|log|E|)$

### 拓扑排序

![image-20250510204413473](images/image-20250510204413473.png)

AOV(activity On Vertex)

拓扑序：如果图中从v到w有一条有向路径，则v一定排在w之前。满足此条件的顶点序列称为一个拓扑序

获取一个拓扑序的过程就是拓扑排序

AOV如果有合理的拓扑序，则必定是有向无环图(Directed Acyclic Graph,DAG)

![image-20250510205059345](images/image-20250510205059345.png)

算法

```c
void TopSort()
{
    for(cnt=0;cnt<|V|;cnt++){
        V=为输入的入度为0的点;
        if(这样的V不存在){
            Error("图中有回路");
        	break;
        }
        输出V，记录V的输出编号
        for(V的每个邻接点W)
            indegree[W]--;
    }
}
```

$T=O(|V|^2)$

改进

- 随时将被入度变为0的顶点放到一个容器里

```c
void TopSort()
{
    for(图中的每个顶点V)
        if(indegree[V]==0)
            Enqueue(V,Q);
    while(!IsEmpty(Q)){
        V=Dequeue(Q);
        输出V，或者记录V的输出序号;cnt++;
        for(V的每个邻接点W)
            if(--Indegree[W]==0)
                Enqueue(W,Q);
    }
    if (cnt!=|V|)
        Error ("图中有回路")
}
```

$T=O(|V|+|E|)$

### 关键路径问题

AOE(Activity On Edge)网络

一般用于安排项目的工序

![image-20250510211134283](images/image-20250510211134283.png)

![image-20250510211540056](images/image-20250510211540056.png)

![image-20250510212240890](images/image-20250510212240890.png)

有绝对不允许延误的活动组成的路径

整个工期有多长
$Earliest[8]=18$
$Earliest[0]=0$
$Earliest[j]=\underset{<i,j>\in E}{max}\{Earliest[i]-C_{<i,j>}\}$

那几个组有机动时间

$D_{<i,j>}=Latest[j]-Earliest[i]-C_{<i,j>}$
$Latest[8]=18;$
$Latest[i]=under{<i,j>\in E}{min}\{Latest[j]-C_{<i,j>}\}$

### 例：旅游规划

![image-20250510213510547](images/image-20250510213510547.png)

城市为结点

公路为边<br>权重1：距离
权重2：收费

单源最短路
Dijkstra—距离
等距离时按收费更新

```c
void Dijkstra(Vertex s)
{
    while(1){
        V=未收录顶点中dist最小者;
        if(这样的V不存在)
            break;
        collected[V]=true;
        for(V的每个邻接点W)
            if(collected[W]==false)
                if(dist[V]+E<v,w><dist[W]){
                    dist[W]=dist[V]+E<v,w>;
                    path[W]=V;
                    cost[W]=cost[V]+C<v,w>
                }
        		else if ((dist[V]+E<v,w>==dist[W])&&(cost[V]+C<v,w><cost[W]){
                    cost[W]=cost[V]+C<v,w>;
                    path[W]=V;       
                        }
    }
}//不能解决有负边的情况
```

要求数最短路径有多少条

- count[s]=1;
- 如果找到更短路：count[W]=count[V];
- 如果找到等长路：count[W]+=count[V];

要求边数最短路

- count[s]=0;
- 如果找到更短路：count[W]=count[V]+1;
- 如果找到等长路：count[W]=count[V]+1;

# 算法

## 概述

```c
void X_sort(ElementType A[],int N)
```

大多数情况下，为简单起见，讨论从小到大的整数排序

N是正整数
只讨论基于排序的比较（> = < 有定义）
只讨论内部排序
稳定性：任何两个相等的数据，排序前后的相对位置不发生改变

没有一种排序是任何情况下都表现最好的

## 基础排序

### 冒泡排序

![](images/2.gif)

```c
void Bubble_Sort(ElementType A[], int N)
{
    for(P=N-1;P>=0;p--){
        flag = 0;
        for(i=0;i<P;i++){//一趟冒泡
            if(A[i]>A[i+1]){
                Swap(A[i],A[i+1]);
                flag = 1;//标识发生了交换
            }
        }
        if(flag==0) break;//全程无交换
    }
}

```

稳定
最好情况：顺序$T=O(N)$
最坏情况：逆序$T=O(N^2)$

### 插入排序

![](images/1.gif)

```c
void Insertion_Sort(ElementType A[],int N)
{
    for(P=1;P<N;P++){
        Tmp=A[P];//摸下一张牌
        for(i=P;i>0 && A[i-1]>Tmp;i--)
            A[i]=A[i-1];//移出空位
        A[i]=Tmp;//新牌落位
    }
}
```

稳定
最好情况：顺序$T=O(N)$
最坏情况：逆序$T=O(N^2)$

### 时间复杂度下限

对于下标$i<j$,如果A[i]>A[j],则称$(i,j)$是一对逆序对
交换两个元素正好消去以个逆序对
插入排序：$T(N,I)=O(N+I)$
				——如果序列基本有序，则插入排序简单且高效

定理：任意N个不同元素组成的序列平均具有$N(N-1)/4$个逆序对

定理：任何仅以交换相邻两元素来排序的算法，其平均时间复杂度为$\varOmega(N^2)$

这意味着：要提高算法效率，我们必须

- 每次消去不止1个逆序对
- 每次交换间隔较远的两元素

### 希尔排序

![image-20250512174243844](images/image-20250512174243844.png)

定义增量序列$D_M>D_{M_1}>...>D_1=1$
对每个$D_K$进行“$D_K-$间隔”排序
注意：“$D_K-$间隔”有序的序列，在执行“$D_K-$间隔”排序后，仍然是“$D_K-$间隔”有序的

#### 希尔增量序列

原始希尔排序 $D_M=[N/2],D_k=[D_{k+1}/2]$

```c
void Shell_sort(ElementType A[],int N)
{
    for(D=N/2;D>0;D/=2){//希尔增量序列
        for(P=D;P<N;P++){//插入排序
            Tmp=A[P];
            for(i=P;i>=D && A[i-D]>Tmp;i-=D)
                A[i] = A[i-D];
            A[i]=Tmp
        }
    }
}
```

最坏情况：$T=\varTheta(N^2)$

#### 更多增量序列

Hibbard增量序列

- $D_K=2^k-1$——相邻元素互质
- 最坏情况：$T=\varTheta(N^{3/2})$
- 猜想：$T_{avg}=O(N^{5/4})$

Sedgewick增量序列

- {1，5，19，41，109，...}

    ——$9\times4^i-9\times2^i+1或4^i-3\times2^i+1$

- 猜想：$T_{avg}=O(N^{7/6}),T_{worst}=O(N^{4/3})$

### 选择排序

![](images/4.gif)

```c
void Selection_Sort(ElementType A[],int N)
{
    for(i=0;i<N;i++){
        MinPosition = ScanForMin(A,i,N-1);
        //从A[i]到A[N-1]中找最小元
        Swap(A[i],A[MinPosition]);
        //将未排序部分的最小元换到有序部分的最后位置
    }
}
```

无论如何：$T=\varTheta(N^2)$

### 堆排序

算法1

```c
void Heap_Sort(ElementType A[],int N)
{
    BuildHeap(A);//O(N)
    for(i=0;i<N;i++)
        TmpA[i]=DeleteMin(A);//O(logN)
    for(i=0;i<N;i++)//O(N)
        A[i]=TmpA[i];
}
```

T(N)=O(N logN)

需要额外O(N)空间，并且复制元素需要时间

算法2

![image-20250512204210320](images/image-20250512204210320.png)

```c
void Heap_Sort(ElementType A[],int N)
{
    for(i=N/2;i>=0;i--)//BuildHeap
         PercDown(A,i,N);
    for(i=N-1;i>0;i--){
         Swap(&A[0],&A[i]);//DeleteMax
		PercDown(A,0,i);
    }
}
```

定理：堆排序处理N个不同元素的随机排列的平均比较次数是$2NlogN-O(NloglogN)$

虽然对排序给出最佳平均时间复杂度，但实际效果不如用Sedgewick增量序列的希尔排序

### 归并排序

核心：有序子列的归并

![image-20250512205129081|700x430](images/image-20250512205129081.png)

如果两个子列一公有N个元素，则归并的时间复杂度是：$T(N)=O(N)$

```c
//L=左边起始位置 , R=右边起始位置 ,RightEnd=右边终止位置
void Merge(ElementType A[],ElementType TmpA[],int L, int R, int RightEnd)
{
    LeftEnd = R-1;//左边终点位置，假设左右两列挨着
    TmpA=L;//存放结果的数组的初始位置
    NumElements=RightEnd - L + 1;
    while(L<=LeftEnd && R<=RightEnd){
        if(A[L]<=A[R])TmpA[Tmp++]=A[L++];
        else		 TmpA[Tmp++]=A[R++];
    }
    while(L<=LeftEnd)//直接复制左边剩下的
        TmpA[Tmp++]=A[L++];
    while(R<=RightEnd)//直接复制右边剩下的
        TmpA[Tmp++]=A[R++];
    for(i=0;i<NumElements;i++,RightEnd--)
        A[RightEnd]=TmpA[RightEnd];
}
```

#### 递归算法

分而治之

![image-20250512213605682](images/image-20250512213605682.png)

```c
void Msort(ElementType A[],ElementType TmpA[],int L, int RightEnd)
{
    int Center;
    if(L<RightEnd){
        Center=(L+RightEnd)/2;
        MSort(A,TmpA,L,Center);
        MSort(A,TmpA,Center+1,RightEnd);
        Merge(A,TmpA,L,Center+1,RightEnd);
    }
}
```

稳定
$T(N)=T(N/2)+T(N/2)+O(N)\rightarrow T(N)=O(NlogN)$

统一函数接口

```c
void Merge_sort(ElementType A[],int N)
{
    ElementType *TmpA;
    TmpA=malloc(N*sizeof(ElementType));
    if(TmpA !=NULL){
        Msort(A,TmpA,0,N-1);
        free(TmpA);
    }
    else Error("空间不足");
}
```

如果只在Merge中声明临时数组

```c
void Merge(ElementType A[], int L,int R,int RightEnd)
    
void Merge(ElementType A[],int L,int RightEnd)    
```

![image-20250512215805783](images/image-20250512215805783.png)

#### 非递归算法

![image-20250512220209814](images/image-20250512220209814.png)

```c
void Merge_pass(ElementType A[],ElementType TmpA[],int N,int length)//length=当前有序子列的长度
{
    for(i=0;i<=N-2*length;i+=2*length)
        Mergel(A,TmpA,i,i+length,i+2*length-1);
    if(i+length<N)//归并最后两个子列
        Mergel(A,TmpA,i+length,N-1);
    else//最后一个子列
        for(j=i;j<N;j++)TmpA[j]=A[j];
}
```

将A中元素归并到TmpA

```c
void Merge_sort(ElementType A[],int N)
{
    int length = 1;//
    ElementType *TmpA;
    TmpA=malloc(N*sizeof(ElementType));
    if(TmpA !=NULL){
        while (length<N){
            Merge_pass(A,TmpA,N,length);
            length*=2;
            Merge_pass(TmpA,A,N,length);
            length*=2;
        }
    
    free(TmpA)
    }
    else Error("空间不足")
}
```

稳定

## 高级排序

### 快速排序

#### 分而治之

![image-20250515212432836](images/image-20250515212432836.png)

```c
void Quicksort(elementType  A[],int N)
{
    pivot = 从A[]中选一个主元;
    将S={A[]\pivot}分成两个独立子集:
    	A1={a∈S|a<=pivot}和
        A2={a∈S|a>=pivot};
	A[]=Quicksort(A1,N1)∪
    			{pivot}∪
        Quicksort(A2,N2)
}
```

排序算法的最好情况
每次正好中分$\rightarrow T(N)=O(NlogN)$

#### 选主元

$$
令pivot = A[0]\\
1 2 3 4 5 6 ... N-1 N\\
 2 3 4 5 6 ... N-1N\\
 3 4 5 6 ... N-1N\\
 
 T(N)=O(N)+T(N-1)\\
 =O(N)+O(N-1)+T(N-2)\\
 =O(N)+O(N-1)+O(N-2)...+O(1)\\
 =O(N^2)
$$

选主元

取头、中、尾、的中位数

```c
ElementType Median3(ElementType A[],int left,int right)
{
    int center=(left+right)/2;
    if(A[Left]>A[Center])
        Swap(&A[Left],&A[Center]);
    if(A[Left]>A[Right])
        Swap(&A[Left],&A[Right]);
    if(A[Center]>A[Right])
        Swap(&A[Center],&A[Right]);
    //A[left]<=A[center]<A[Right]
    Swap(&A[Center],&A[Right-1]);//将pivot藏到右边
    //只需要考虑A[Left+1]..A[Right-2]
    return A[Right-1]
}
```

#### 小规模数据的处理

快速排序的问题

- 用递归
- 对小规模的数据（例如N不到100）可能还不如插入排序快

解决方案

- 递归数据规模充分小，则停止递归，直接调用简单排序
- 在程序中定义一个Cutoff的阈值

#### 算法实现

```c
void Quicksort(ELementType A[],int Left,int Right)
{	
    if(Cutoff<=Right-left){
    	pivot=Median3(A,left,Right);
 		i=Left;j=Right-1;
        for(;;){
            while(A[++i]<pivot){}
            while(A[--j]>pivit){}
            if(i<j)
                Swap(&A[i],&A[j]);
            else break;
        }
        Swap(&A[i],&A[Right-1]);
        Quicksort(A,Left,i-1);
        Quicksort(A,i+1,Right);
    }
    else
        Insertion_Sort(A+Left,Right-Left+1);
 
}

void Quick_Sort(ELementType A[],int N)
{
    Quicksort(A,0,N-1);
}
```

### 表排序

#### 算法概述

定义一个指针数组作为“表”(table)

![image-20250516192334724](images/image-20250516192334724.png)

如果仅按顺序输出，则输出：
$A[table[0]],A[table[1]],...A[table[N-1]]$

#### 物理排序

- N个数字的排列由若干个独立的换组成

![image-20250516193240348](images/image-20250516193240348.png)

Temp=f
如何判断一个环的结束
if(table[i]==i)

#### 复杂度分析

最好的情况：初始即有序
最坏的情况：

- 有$[N/2]$个换，每个环包含两个元素
- 需要$[3N/2]$次元素移动

$T=O(mN),m$是每个元素的复制时间

### 基数排序

#### 桶排序

例：假设我们有N个学生，他们的成绩是0-100之间的整数（于是有M=101个不同的成绩值）。如何在线性时间内将学生按成绩排序？

![image-20250516194423054](images/image-20250516194423054.png)

```c
void Bucket_Sort(ElementType A[], int N)
{
    count [] 初始化;
    while(读入1个学生成绩grade)
        将该生插入count[grage]链表;
    for( i=0; i<M ; i++ ){
        if( count[i] )
            输入整个count[i]链表;
    }
}
```

$T(N,M)=O(M+N)$

#### 基数排序

例：假设我们有10个整数，他们的值是0-999之间的整数（于是有M=1000个不同的值）。如何在线性时间内将学生按成绩排序？

输入序列：64,8,216,512,27,729,0,1,343,125
用“次位优先”(Least Signnificant Digit)
![image-20250516195222620](images/image-20250516195222620.png)

$T=O(P(N+B))$

#### 多关键字的排序

例：一副扑克牌是按2种关键字排序的
![image-20250516195512128](images/image-20250516195512128.png)

- 用“主位优先”（Most Significant Digit）排序：为花色建4个桶
    ![image-20250516195727933](images/image-20250516195727933.png)
    在每个桶内分别排序，最后合并结果
- 用“次位优先”(Least Signnificant Digit)排序：为面值建13个桶
    ![image-20250516201155761](images/image-20250516201155761.png)
    将结果合并，然后为花色建4个桶
- LSD与MSD在不同情况下速度各有优劣

### 算法排序的比较

| 排序方法   | 平均时间复杂度     | 最坏情况下的时间复杂度 | 额外空间复杂度   | 稳定性 |
| ------ | ----------- | ----------- | --------- | --- |
| 简单选择排序 | $O(N^2)$    | $O(N^2)$    | $O(1)$    | 不稳定 |
| 冒泡排序   | $O(N^2)$    | $O(N^2)$    | $O(1)$    | 稳定  |
| 直接插入排序 | $O(N^2)$    | $O(N^2)$    | $O(1)$    | 稳定  |
| 希尔排序   | $O(N^d)$    | $O(N^2)$    | $O(1)$    | 不稳定 |
| 堆排序    | $O(NlogN)$  | $O(NlogN)$  | $O(1)$    | 不稳定 |
| 快速排序   | $O(NlogN)$  | $O(N^2)$    | $O(logN)$ | 不稳定 |
| 归并排序   | $O(NlogN)$  | $O(NlogN)$  | $O(N)$    | 稳定  |
| 基数排序   | $O(P(N+B))$ | $O(P(N+B))$ | $O(N+B)$  | 稳定  |

## 查找

### 散列表

已知几种查找方法：

- 顺序查找										$O(N)$
- 二分查找										$O(log_2N)$
- 二叉搜索树									 $O(h)$h为二叉搜索树的高度
  平衡二叉树									 $O(log_2N)$

例：在登录QQ的时候，QQ服务器是如何核对你的身份？面对庞大的用户群，如何快速找到用户信息

是否可以用二分法查找

十亿有效用户，用二分查找30次
十亿$\times$1K$\approx$1024G,1T连续空间
按有效QQ号大小有序存储：在连续存储空间中，插入和删除一个新QQ号码需要大量移动数据

【问题】如何快速搜索到需要的关键词？如果关键次不方便怎么办
查找的本质：从已知对象找位置

- 有序安排对象：全序、半序
- 直接“算出”对象位置：散列

散列查找放的两项基本工作：

- 计算位置：构造散列函数确定关键次存储位置
- 解决冲突：应用某种策略解决多个关键词位置相同的问题

时间复杂度几乎是常量：$O(1)$，即查找时间与问题规模无关

#### 抽象数据类型表述

```
类型名称：符号表(SymbolTable)
    
数据对象即：符号表是“名字(Name)-属性(Attribute)”对的集合

操作集：Table∈SymbolTable，Name∈NameType，Attr∈Attribute Type
1、SymbolTable InitalizeTable(int TableSize):
创建一个长度为TableSize的符号表;
2、Boolean IsIn(SymbolTable Table,NameType Name):
获取特定的名字Name是否在符号表Table中;
3、AttributeType Find(SymbolTable Table,NameType Name):
将Table中指定名字Name对应的属性;
4、SymbolTable Modefy(SymbolTable Table,NameType Name,AttributeType Attr):
将Table中指定名字Name的属性修改为Attr;
5、SymbolTable Insert(SymbolTable Table,NameType Name,AttributeType Attr):
向Table中插入一个新名字Name及其属性Attr;
6、SymbolTable Delete(SymbolTable Table,NameType Name):
从Table中删除一个名字Name及其属性
```

例：有拿1个数据随想的集合{18，23，11，20，2，7，27，30，42，15，34}

​	符号表大小用TableSize=17，选取的散列函数h如下：
​	$h(key)=key\,\, mod\,\,TableSize$

| 地址   | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   | 15   | 16   |
| ------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 关键词 | 34   | 18   | 2    | 20   |      |      | 23   | 7    | 42   |      | 27   | 11   |      | 30   |      | 15   |      |

存放：

$h(18)=1,h(23)=6,h(11)=11,h(20)=3,h(2)=2,......$
如果新插入35，h(35)=1,该位置已有对象，冲突

查找：

key=22,h(22)=5,该地址为空，不在表中
key=30,h(30)=13,该地址存放的是30，找到

装填因子（Loading Factor）：设散列表大小为m，填入表中的元素个数是n，则称$\alpha=n/m$为散列表的装填因子
$\alpha=11/17\approx0.65$

【例】将acos、define、float、exp、char、atan、ceil、floor、clock、ctime顺序存入一张散列表
散列表设计为一个二维数组Table\[26][2],2列分别代表2个槽

如何设计散列函数h(key)=?
h(key)=key[0]-'a'

|        | 槽0    | 槽1   |
| ------ | ------ | ----- |
| 0      | acos   | atan  |
| 1      |        |       |
| 2      | char   | ceil  |
| 3      | define |       |
| 4      | exp    |       |
| 5      | float  | floor |
| 6      |        |       |
| ...... |        |       |
| 25     |        |       |

如果没有溢出
$T_{查询}=T_{插入}=T_{删除}=O(1)$

"散列(Hashing)"的基本思想是

1. 以关键字key为自变量，确定一个确定函数h(散列函数),计算出对应函数值h(key),作为数据对象的存储地址
2. 可能不同关键字会映射到同一个散列地址上即$h(key_i)=h(key_j)$(当$hey_i\ne hey_j$),称为“冲突(Collision)”。——需要某种冲突解决策略

### 散列函数构造

#### 数字关键词的散列函数构造

1. 直接定址法
    取关键词的某个线性函数值为散列地址，即
    $h(key)=a\times key +b\,\,\,\,\,\,(a,b为常数)$

    | 地址h(key) | 出生年份 | 人数(attribute) |
    | ---------- | -------- | --------------- |
    | 0          | 1990     | 1285万          |
    | 1          | 1991     | 1281万          |
    | 2          | 1992     | 1280万          |

2. 除留余数法
    散列函数为：$h(key)=key\,\, mod \,\,p$
    这里：p=Tablesize=17
    一般，p取素数

3. 数字分析法

    分析数字关键字在各位上的变化情况，去比较随机的位作为散列地址

    比如：取11位手机号码key的后4位作为地址：
    散列函数为：$h(key)=atoi(key+7)\,\,\,\,(char *key)$

    如果关键词key是18位的身份证号码：

    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   | 15   | 16   | 17   | 18   |
    | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | 3    | 3    | 0    | 1    | 0    | 6    | 1    | 9    | 9    | 0    | 1    | 0    | 0    | 8    | 0    | 4    | 1    | 9    |
    |      | 省 |      | 市 |      | 区 |      |      |      | 年 |      | 月 |      | 日 |      |      | 序号 | 校验 |

4. 折叠法

    把关键词分割成位数相同的几个部分然后叠加

5. 平方取中法

    让尽可能多的位参与影响

#### 字符关键词的散列函数构造

1. 一个简单的散列函数——ASCII码加和法
    对字符型关键词key的散列函数如下:
    $h(key)=(\varSigma key[i])mod \,\,TableSize$
2. 简单的改进——前三个字符移位法
    $h(key)=(key[0]\times 27^2+key[1]\times27+key[2])mod\,\, TableSize$
3. 好的散列函数——移位法
    涉及关键词所有n个字符，并且分布得很好
    $h(key)=(\underset{i=0}{\overset{n-1}\varSigma}[n-i-1]\times32^i)mod\,\,TableSize$

快速计算：

$h（'abcde'）='a'\times32^4+'b'\times32^3+'c'\times32^2+'d'\times32+'e'$

$(a\times32+b)\times32+c...$

$x\times32:x<<5$

```c
Index Hash(const char *Key, int TableSize)
{
    unsigned int h=0;//散列函数值，初始化为0
    while(*Key!='\0')//位移映射
        h=(h<<5)+*Key++;
    return h%TableSize;
}
```

### 冲突处理的方法

常用处理冲突的思路

- 换个位置：开放寻址法
- 同一位置的冲突对象组织在一起：链地址法

#### 开放定址法（Open Addressing）

一旦发生了冲突（该地址已有其他元素），就按某种规则去寻找另一空地址

若发生第i次冲突，试探的下一个地址将增加$d_i$,基本公式是：$h_i(key)=(h(key)+d_i)\,\,mod\,\,TableSize\,\,\,\,(1\le i <TableSzie)$

$d_i$决定了不同的解决冲突的方案：线性探测（$d_i=i$），平方探测($d_i=\pm i^2$)，双散列($d_i=i\times h_2(key))$)

1. 线性探测法（Linear Probing）
    以 增量序列$1,2,3,......(TableSize-1)$循环试探下一个存储地址
    例设关键词序列{47，7，29，11，9，84，54，20，30}
    散列表长TableSize=13（装填因子$\alpha=9/13\approx0.69$）
    散列函数为：h(key)=key mod 11
    用线性探测法处理冲突，列出依次插入后的散列表，并估算查找性能

    | 关键词（key）    | 47   | 7    | 29   | 11   | 9    | 84   | 54   | 20   | 30   |
    | ---------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | 散列地址h（key） | 3    | 7    | 7|0| 9 | 7    | 10  | 9  | 8   |
    | 冲突次数 | 0 | 0 | 1 |0| 0 | 3 | 1 | 3 | 6 |
    
    ![image-20250517112922309](images/image-20250517112922309.png)
    注意聚集现象
    散列表性能分析
    
    - 成功平均查找长度（ASLs）
    - 不成功平均查找长度（ASLu）
    
    散列表：
    
    | H(key)   | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   |
    | -------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | key      | 11   | 30   |      | 47   |      |      |      | 7    | 29   | 9    | 84   | 54   | 20   |
    | 冲突次数 | 0    | 6    |      | 0    |      |      |      | 0    | 1    | 0    | 3    | 1    | 3    |
    
    ASLs：查找表中关键词的平均查找比较次数（其冲突次数加1）
    ASLs=（1+7+1+1+2+1+4+2+4）/9=23/9$\approx$2.56
    ASLu:不在散列表中的关键词的平均查找次数
    一般方法：将不在散列表中的关键词分若干类
    如：根据H（key）值分类
    ASLu=（3+2+1+2+1+1+1+9+8+7+6）/11=41/11$\approx$3.73
    散列函数h(key)=key mod 11
    因此，分为11类分析
    
    例将acos、define、float、exp、char、atan、ceil、floor
    顺次存入一张大小为26的散列表中。
    
    H(key)=key[0]-'a'，采用线性探测$d_i=i$
    
    | acos | atan | char | define | exp  | float | ceil | floor |      | ...... |      |
    | ---- | ---- | ---- | ------ | ---- | ----- | ---- | ----- | ---- | ------ | ---- |
    | 0    | 1    | 2    | 3      | 4    | 5     | 6    | 7     | 8    |        | 25   |
    
    ASLs:表中关键字的平均查找比较次数
    ASLs=(1+1+1+1+1+2+5+3)/8=15/8$\approx$1.87
    ASLu:不在散列表中的关键次的平均查找次数（不成功）
    根据H(key)值分为26种情况：H的值为0、1、2...、25
    
    ASLu=(9+8+7+6+5+4+3+2+1*18)/26=62/26$\approx$2.38
    
2. 平方探测法(Quadratic Probing)——二次探测
    平方探测法：一增量序列$1^2,-1^2,2^2,-2^2,......,q^2,-q^2且q\le[TableSize/2]$循环试探下一个存储地址
    设关键词序列为{47，7，29，11，9，84，54，20，30}
    散列表长TableSize=11
    散列函数为：h(key)=key mod 11
    桶平方探测法处理冲突，列出依次插入后的散列表，并估算ASLs

    | 关键词key      | 47   | 7    | 29   | 11   | 9    | 84   | 54   | 20   | 30   |
    | -------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | 散列地址h(key) | 3    | 7    | 7    | 0    | 9    | 7    | 10   | 9    | 8    |
    | 冲突次数       | 0    | 0    | 1    | 0    | 0    | 2    | 0    | 3    | 3    |

    ![image-20250517122421600](images/image-20250517122421600.png)
    ASLs=（1+1+2+1+1+3+1+4+4)/9=18/9=2
    二次探测寻找空间
    ![image-20250517123022843](images/image-20250517123022843.png)

    有定理显示：如果散列表长度TableSize是某个4k+3（k是正整数）行式的素数下hi，平方探测法就可以探查到整个散列表空间
    平方探测法的实现

    ```c
    typedef struct HashTbl *HashTable;
    struct HashTbl{
        intTableSize;
        Cell *TheCells;
    }H;
    HashTable Initialize Table(int TableSize)
    {
        HashTable H;
        int i;
        if(TableSize<MinTableSize){
            Error("");
            return NULL;
        }
        //
        H=(HashTable)malloc(sizeof(Struct HashTbl));
        if(h==NULL)
            FatalError("空间溢出!!!");
        H->TableSize=NextPrime(TableSize);
        //
        H->TheCells=(Cell*)malloc(sizeof(Cell)*H->TableSize);
        if(H->TheCells==NULL)
            FatalError("空间溢出!!!");
        for(i=0;i<H->TableSize;i++)
            H->TheCells[i].Info=Empty;
        return H;
    }
    ```

    ​	![image-20250517174314294](images/image-20250517174314294.png)

    ```c
    Position Find(ElementType Key,HashTable H)//平方探测
    {
        Position CurrentPos,NewPos;
        int CNum;//记录冲突次数
        CNum = 0;
        NewPos = CurrentPos = Hash(key,H->TableSize);
        while(H->TheCells[NewPos].Info!=Empty&&H->TheCells[NewPos].ElementType!=Key){
            //字符串类型的关键词需要strcmp函数!!
            if(++CNum%2){//判断冲突的奇偶次
                NewPos=CurrentPos+(CNum+1)/2*(CNum+1)/2;
                while(NewPos>=H->TableSize)
                    NewPos -= H->TableSize;
            }else{
                NewPos = CurrentPos - CNum/2*CNum/2;
                while(NewPos<0)
                    NewPos+=H->TableSize;
            }
        }
        return NewPos;
    }
    ```

    | $d_i$ | $+1^2$ | $-1^2$ | $+2^2$ | $-2^2$ | $+3^2$ | $-3^2$ |
    | ----- | ------ | ------ | ------ | ------ | ------ | ------ |
    | Cnum  | 1      | 2      | 3      | 4      | 5      | 6      |

    ```c
    void Insert(ElemntType Key,HashTable H)
    {//插入操作
        Position Pos;
        Pos=Find(Key,H);
        if(H->TheCells[Pos].Info!=Legitimate){
            //确认在此插入
            H->TheCells[Pos].Info=Legitmate;
            H->TheCells[Pos].Element=Key;
            //字符串类型的关键词需要strcpy函数！！
        }
    }
    ```

    在开放地址散列表中，删除操作要很小心。通常只能“懒惰删除”，既需要增加一个“删除标记（Deleted）”，并不是真正删除它。以便查找时不会“断链”其空间可以在下次插入时重用

3. 双散列探测法（Double Hashing）
    双散列探测法：$d_i$为$i\times h_2(key),h_2(key)$时另一个散列函数
    探测序列成：$h_2(key),2h_2(key),3h_2(key)...$

    对任意的key，$h_2(key)\ne 0!$

    探测序列还应该保证所有的散列序列存储单元都应该能够被探测到。选择以下形式有良好的效果：
    $h_2(key)=p-(key\,\,mod\,\,p)$
    其中：p<TableSize,p、TableSize都是素数

4. 再散列（Rehashing）

    - 当散列表元素太多时（即装填因子$\alpha$太大）时，查找效率会下降
        - 实用最大装填因子一般取0.5<=$\alpha$<=0.85
    - 当装填因子过大时，解决的方法时加倍扩大散列表，这个过程叫“再散列（Rehashing）”

#### 分离链接法（Separate Chaining）

分离链接法：将相同位置上冲突的所有关键词存储再同一个但链表中

例：设关键词序列为47，7，29，11，16，92，22，8，3，50，37，89，94，21；散列函数取为：h(key)=key mod 11;用分离链接法处理冲突

```c
typedef HashTbl{
    int TableSizel;
    List TheLists;
}*H
```

![image-20250518104345659](images/image-20250518104345659.png)

- 表中9个结点只需要1次查找

- 5个结点需要两次查找

- 查找成功的平均次数

    ASL s=(9+5*2)/14$\approx$1.36

```c
typedef struct ListNode *Position,*List;
struct ListNode{
    ElementType Element;
    Position Next;
};
typedef struct HashTbl *HashTable;
struct HashTbl{
    int TableSize;
    List TheLists;
};
Position Find(ElementType Key,HashTable H)
{
    Position P;
    int Pos;
    
    Pos = Hash(key,H->TableSize);//
    P=H->TheLists[Pos].Next;//
    while(P!=NULL && strcmp(P->Element,Key))
        P=P->Next;
    return P;   
}
```

#### 散列表性能分析

平均查找长度（ASL）用来度量散列表查找效率：成功、不成功

关键词的比较次数，取决于产生冲突的多少，影响产生冲突有以下三个因素：

-  散列函数是否均匀

-  处理冲突的方法

-  散列表的装填因子$\alpha$

     

1.  线性探测法的查找性能
        期望探测次数满足以下公式

    $p=\begin {cases}\underset{2}{1}[1+\underset{{(1-\alpha)^2}}{1}](对插入和不成功查找而言)\\\underset{2}{1}(1+\underset{(1-\alpha)}{1}(对成功查找而言)\end{cases}$

    当$\alpha$=0.5时，
    插入操作和不成功查找的期望$ASL u=0.5*(1+1/(1-0.5)^2)=2.5 $次
    成功查找的期望$ASLs = 0.5*(1+1/(1-0.5))=1.5$次

    | H(key)   | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   |
    | -------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | key      | 11   | 30   |      | 47   |      |      |      | 7    | 29   | 9    | 84   | 54   | 20   |
    | 冲突次数 | 0    | 6    |      | 0    |      |      |      | 0    | 1    | 0    | 3    | 1    | 3    |

    $\alpha$​=9/13=0.69,于是
    期望$ASLu=0.5*(1+1/(1-0.69)^2)=5.70 $次
    成功查找的期望$ASLs = 0.5*(1+1/(1-0.69))=2.11$次
    (实际计算ASLs=2.56)

4. 平方探测法和双散列探测法的查找性能
    可以证明，平方探测法和双散列探测法探测次数满足下列公式：
    $p=\begin {cases}\underset{{(1-\alpha)}}{1}(对插入和不成功查找而言)\\-\underset{\alpha}{1}ln(1-\alpha)(对成功查找而言)\end{cases}$​

    当$\alpha$=0.5时，
    插入操作和不成功查找的期望$ASL u=0.5*(1+1/(1-0.5))=2 $次
    成功查找的期望$ASLs = -1/0.5*ln(1-0.5)\approx 1.39$次
    
    | H(key)   | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   |
    | -------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | key      | 11   | 30   | 20   | 47   |      |      | 84   | 7    | 29   | 9    | 54   |
    | 冲突次数 | 0    | 3    | 3    | 0    |      |      | 2    | 0    | 1    | 0    | 0    |
    
    $\alpha$=9/11=0.82,于是
    期望$ASLu=0.5*(1+1/(1-0.82))\approx5.56 $次
    成功查找的期望$ASLs = -1*0.5*ln(1-0.5))\approx2.09$次
    (实际计算ASLs=2)
    
    期望探测次数与装填因子$\alpha$的关系
    ![image-20250518113036491](images/image-20250518113036491.png)

3. 分离链接法的平均性能
    $p=\begin {cases}\alpha+e^{-\alpha}(对插入和不成功查找而言)\\1+\underset{\alpha}{2}(对成功查找而言)\end{cases}$

    当$\alpha$=0.5时，
    插入操作和不成功查找的期望$ASL u=1+e^{-1}=2 $次
    成功查找的期望$ASLs = 1+1/2 =1.5$次
    前面的例子14个元素分布在11个单链表中，所以$\alpha$=14/11$\approx$​1.27
    期望$ASLu=1.27+e^{-1.27}\approx5.56 $次
    成功查找的期望$ASLs = 1+12.7/2\approx1.64$次
    (实际计算ASLs=1.36)

选择合适的h(key),散列法的查找效率期望是常数$O(1)$,他几乎与关键字的空间的大小n无关！也适合于关键字直接比较计算量大的问题

他是以较小的$\alpha$为前提。因此，散列方法一个以空间换时间

散列方法的存储对关键字是随机的，不便于顺序查找关键字，也不适合于范围查找，或最大最小值查找

开放地址法：

- 散列表是一个数组，存储效率高，随机查找
- 散列表有聚集现象

分离链表法

- 散列表是顺序存储于链式存储的结合，链表部分的存储效率和查找效率都较低
- 关键字删除不需要“懒惰删除”法，从而没有存储“垃圾”
- 太小的$\alpha$肯导致空间浪费，大的$\alpha$又将付出更多的时间代价。不均匀长的链表的长度导致时间效率的严重下降

### 例：文件中单词词频统计

给定一个英文文本文件，统计文件中所有单词出现的频率，并输出词频最大的前10%的单词及其词频

假设单词字符定义为大小写字母、数字、下划线，其他字符均仍未是分割符，不予考虑

对新读入的单词在已有的单词表中查找，如果已经存在，则将该单词的词频加1，如果不存在，则插入该单词并记词频为1

散列表

```c
int main(){
    int TableSize = 10000;//散列表的估计大小
    int wordcount = 0,length;
    HashTable H;
    ElemenType word;
    FILE *fp;
    char document[30]="HarryPotter.txt";//要被统计词频的文件名
    H=Initialize Table(TableSize);//建立散列表
    if((fp=fopen(document,'r'))==NULL)FatalError("无法打开文件!\n");
    while(!feof(fp)){
        length=GetAWord(fp,word);//从文件中读取一个词
        if(length > 3){//只考虑适当长度的单词
            wordcount++;//统计文件中的单词总数
            InsertAndCount(word,H)
        }
    }
    fclose(fp);
    printf("%d,",wordcount);
    Show(H,10.0/100);//显示词频前10%的所有单词
    DestoryTable(H);//销毁散列表
    return 0;
        
}
```

### 例：电话聊天狂人

#### 解法分析

![image-20250518153037670](images/image-20250518153037670.png)

##### 解法1——排序

1. 读入最多$2\times10^5$个电话号码，每个号码存为长度11的字符串
2. 按字符串非递减顺序排序
3. 扫描有序数组，累计同号码出现的次数，并且更新最大次数

编程简单快捷

无法拓展解决动态插入的问题

##### 解法2——直接映射

1. 创建有$2*10^{10}$个单元的整数数组，保证每个电话号码对应唯一单元下标：数组初始化为0
2. 对读入的每个电话号码，找到一直为下标的单元，数值累计1次
3. 顺序扫描数组，找到累计次数最多的单元

编程简单快捷，动态插入快

下标超过了unsigned long
		需要$2\times10^{10}\times2bytes\approx37GB$
		为了$2\times10^{5}个号码扫描2^{10}个单元$

##### 解法3——带智商的散列

![image-20250518154639936](images/image-20250518154639936.png)

#### 程序框架搭建

```c
int main ()
{
    创建散列表;
    读入号码插入表中;
    扫描表输出狂人;
    return 0;
}
```

```c
int main()
{
    int N,i;
    ElementType Key;
    HashTable H;
    
    scanf("%d",& N);
    H=CreateTable(N*2);//创建一个散列表
    for(i=0;i<N;i++){
        scanf("%s",Key);Insert(H,Key);
        scanf("%s",Key);Insert(H,Key);
    }
    ScanAndOutput(H);
    DestroyTable(H);
    return 0;
}
```

![image-20250518155350381](images/image-20250518155350381.png)
					

![image-20250518155409660](images/image-20250518155409660.png)

​	

#### 输出狂人

```c
void ScanAndOutput(HashTable H)
{
    for(i=0;i<H->TableSize;i++){//
        Ptr=H->Heads[i].Next;
        while(Ptr){
            if(Ptr->Count>MaxCnt){//
                MaxCnt=Ptr->Count;
                strcpy(MinPhone,Ptr->Data);
                Pcnt=1;
        }
            else if(Ptr->Count==MaxCnt){
                PCnt++;//
                if(strcmp(minPhone,Ptr->Data)>0)
                    strcpy(Minphone,Ptr->Data);//
            }
            Ptr=Ptr->Next;
    	}
    }
    printf("%s %d",MinPhone,MaxCnt);
    if(PCnt>1) printf("%d",PCnt);
    printf("\n")
}
```

#### 模块的引用和裁剪

```c
#define KEYLENGTH 11//关键词字符串的最大长度
//关键词类型用字符串
typedef char ELementType[KEYLENGTH+1];
typedef int Index;//散列地址类型

typedef struct LNode *PtrToLNode;
struct LNode{
    ElementType Data;
    PtrToLNode Next;
    int Count;
};

typedef struct TblNode *HashTable;
struct TblNode{//散列表结点定义
    int TableSize;//表的最大长度
    List Heads;//指向链表头结点的数组
}
```

```c
#define MAXTABLESIZE 1000000
int NextPrime(int N)
{//返回大于N且不超过MAXTABLESIZE的最小素数
   int i,p=(N%2)?N+2:N+1;//从大于N的下一个奇数开始
    while(p<=MAXTABLESIZE){
        for(i=(int)sqrt(p);i>2;i--)
            if(!(p%i))break;//p不是素数
        if(i==2)break;//for正常结束，说明p是素数
        else p +=2;//否则试探下一个素数
    }
    return p;
}

HashTable CreateTable(int TableSize)
{
    HashTable H;
    int i;
    H=(HashTable)malloc(sizeof(struct TblNode));
    H->TableSize = NextPrime(TableSzie);
    H->Heads = (List)malloc (H->TableSize*sizeof(struct LNode));
    for(i=0;i<H->TableSize;i++){
        H->Heads[i].Data[0]='\0';H->Heads[i].Next = NULL;
        H->Heads[i].Count = 0;
    }
    return H;
}

int Hash (int Key,int P)
{//除留余数法散列函数
    return Key%P;
}
```

```c
#define MAXD 5//参与散列映射计算的字符个数

Position Find(HashTable H,ElementType Key)
{
    Position P;
    Index Pos;
    
    //初始散列位置
    Pos = Hash(atoi(Key+KETLENGTH-MAXD),H->TableSize);
   
    P=H->Heads[Pos].Next;//从该链表的第一个结点开始
    //当未到表尾，并且Key未找到时
    while(P && strcmp(P->Data,Key))
        P=P->Next;
    return P;//此时P或者指向找到的结点，或者为NULL
}
```

```c
bool Insert (HashTable H,ElementType Key)
{
    Position P,NewCell;
    Index Pos;
    if(!P){//关键词未找到，可以插入
        NewCell = (Position) malloc (sizeof(struct LNode)); 
        strcpy(NewCell->Data,Key);
        NewCell->Count = 1;
        Pos=Hash(atoi(Key+KEYLENGTH-MAXD),H->TableSize);
        //将NewCell插入为H->Heads[Pos]链表的第一个结点
        NewCell->Next=H->Heads[Pos].Next;
        H->Heads[Pos].Next=NewCell;
        return true;
    }
    else{//关键词已存在
        P->Count++;
        return false;
    }
}
```

### 例：Insert or Merge

如何区分简单插入和非递归的归并排序

- 插入排序：前面有序，后面没变化
- 归并排序：分段有序

#### 捏软柿子算法

判断是否是插入排序

- 从左向右扫描，直到发现顺序不对，跳出循环
- 从跳出地点继续向右扫描，与原始序列比对，发现不同则判断为“非”
- 循环自然结束，则判断为“是”，返回跳出地点

如果是插入排序，则从跳出地点开始进行一趟插入

判断归并段的长度

最小N应该是多大

- 插入排序第1步，什么都没改变
- 归并排序第1步，什么都变了

尾部子列为u变化，但是前面变了（归并）

### 例：Sort or Swap

给定N个数字的排列，如何仅利用与0交换达成排序目的

- N个数字的排列有若干个独立的环组成

环的分类

1. 只有1个元素：不需要交换
2. 环里$n_0$个元素，包括0：需要$n_0-1$次交换
3. 第i个环例有$n_i$个元素，不包括0：先把0换到环里，再进行$(n_i+1)-1$次交换——一共是$n_i+1$次交换

若N个元素的序列包含S个单元环、K个多元环

$n_0-1+\underset{i=1}{\overset{k-1}{\varSigma}}(n_i+1)$
		$\underset{i=1}{\overset{k-1}{\varSigma}}n_i+K-2=N-S+K-2$

#### 算法示例

| 下标 | [0]  | [1]  | [2]  | [3]  | [4]  | [5]  | [6]  | [7]  | [8]  | [9]  |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A[]  | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |
| T[]  | 7    | 9    | 3    | 0    | 5    | 1    | 4    | 2    | 8    | 6    |

T[A[i]]=i;元素i在A[T[i]]中存放

3+6

N-S+K-2=10-1+2-2=9

### 例：Hashing Hard Version

已知H(x)=x%N以及用线性探测解决冲突问题

先给出散列映射结果，反求输入顺序

当元素x被映射到H(x)位置，发现这个位置已经有yl则y一定是在x之前被输入的

| 下标 | [0]  | [1]  | [2]  | [3]  | [4]  | [5]  | [6]  | [7]  | [8]  | [9]  | [10] |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| H[]  | 33   | 1    | 13   | 12   | 34   | 38   | 27   | 22   | 32   |      | 21   |

![image-20250518181313426](images/image-20250518181313426.png)
1 13 12 21 33 34 38 27 22 32
拓扑排序

### 串的模式匹配

串是线性存储的一串数据（默认是字符）

特殊操作集

- 求串的长度
- 比较两串是否相等
- 两串相接
- 求子串
- 插入子串
- 匹配子串
- 删除子串

给定一段文本，从中找到某个指定关键字

#### 目标

给定一段文本：$string = s_0s_1......S_{n-1}$

给定一个模式：$pattern=p_0p_1......P_{m-1}$

求pattern在string中出现的位置

```c
Position PatternMatch(char *string,char *pattern)
```

1. 方法：C的库函数 strstr

    ```c
    char *strstr(char *string,char *pattern)
    ```

    ```c
    #include<stdio.h>
    #include<string.h>
    
    typedef char* Position;
    #define NotFound NULL
    int main ()
    {
        char string[]= "This is a simple example";
        char pattern[]="simple";
        Position p = strstr(string,pattern);
        if(p==NotFound) printf("Not Found.\n");
        else printf("%s\n",p);
        return 0;
    }
    ```

    ![image-20250518195912155](images/image-20250518195912155.png)
    $T=O(n\cdot m)$

2. 方法：从末尾开始比
    ![image-20250518200235641](images/image-20250518200235641.png)

3. 方法：KMP算法（Knuth、Morris、Pratt）算法
    $T=O(n+m)$
    ![image-20250518202714872](images/image-20250518202714872.png)
    $p=\begin {cases}满足p_0...p_i=P_{j-i}...p_{j}的最大i(<j)\\-1\,\,如果这样的i不存在\end{cases}$

    | pattern | a    | b    | c    | a    | b    | c    | a    | c    | a    | b    |
    | ------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | j       | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |
    | match   | -1   | -1   | -1   | 0    | 1    | 2    | 3    | -1   | 0    | 1    |

#### KMP算法的实现

```c
#include <stdio.h>
#include <string.h>

typedef int Position;
#define NotFound -1

int main()
{
    char string[]= "This is a simple example";
    char pattern[]="simple";
    Position p = KMP(string,pattern);
    if(p==NotFound) printf("Not Found.\n");
    else printf("%s\n",string+p);
    return 0; 
}
```

```c
Position KMP(char *string,char *pattern)
{
    int n = strlen(string);//O(n)
    int m = strlen(pattern);//O(m)
    int s,p,*match;
    if(n<m) return NotFound;
    match = (int *)malloc(sizeof(int)*m);
    BuildMatch(pattern,match);//T_m=O(?)
    s=p=0;
    while(s<n &&p<m){//O(n)
        if(string[s]==pattern[p]){s++,p++;}
        else if (p>0) p=match[p-1]+1;
        else s++;
    }
    return (p==m)?s-m:NotFound
}
```

#### BuildMatch的实现

![image-20250518210349146](images/image-20250518210349146.png)

![image-20250518211032918](images/image-20250518211032918.png)

```c
void BuildMatch(char *pattern ,int *match)
{
    int i, j;
    int m=strlen(pattern);
    match[0]=-1;
    for(j=1;j<m;j++){
        i=match[j-1];
        while((i>=0)&&(pattern[i+1]!=pattern[j]))
            i=match[i];
        if(pattern[i+1]==pattern[j])
            match[j]=i+1;
        else match[j]=-1；
    }
}
```

i回退的总次数不会超过i增加的总次数

$T_m=O(m)$
