## 3、适配器模式

适配器模式可以将一个类的接口转换成客户端希望的另一个接口，使得原来由于接口不兼容而不能在一起工作的那些类可以在一起工作。通俗的讲就是当我们已经有了一些类，而这些类不能满足新的需求，此时就可以考虑是否能将现有的类适配成可以满足新需求的类。适配器类需要继承或依赖已有的类，实现想要的目标接口。

缺点：过多地使用适配器，会让系统非常零乱，不易整体进行把握。比如，明明看到调用的是 A 接口，其实内部被适配成了 B 接口的实现，一个系统如果太多出现这种情况，无异于一场灾难。因此如果不是很有必要，可以不使用适配器，而是直接对系统进行重构。

## 3.1、使用复合实现适配器模式

    
     1 /*
     2 * 关键代码：适配器继承或依赖已有的对象，实现想要的目标接口。
     3 * 以下示例中，假设我们之前有了一个双端队列，新的需求要求使用栈和队列来完成。
     4   双端队列可以在头尾删减或增加元素。而栈是一种先进后出的数据结构，添加数据时添加到栈的顶部，删除数据时先删   除栈顶部的数据。因此我们完全可以将一个现有的双端队列适配成一个栈。
     5 */
     6 ​
     7 //双端队列， 被适配类
     8 class Deque
     9 {
    10 public:
    11     void push_back(int x)
    12     {
    13         cout << "Deque push_back:" << x << endl;
    14     }
    15     void push_front(int x)
    16     {
    17         cout << "Deque push_front:" << x << endl;
    18     }
    19     void pop_back()
    20     {
    21         cout << "Deque pop_back" << endl;
    22     }
    23     void pop_front()
    24     {
    25         cout << "Deque pop_front" << endl;
    26     }
    27 };
    28 ​
    29 //顺序类，抽象目标类
    30 class Sequence  
    31 {
    32 public:
    33     virtual void push(int x) = 0;
    34     virtual void pop() = 0;
    35 };
    36 ​
    37 //栈,后进先出, 适配类
    38 class Stack:public Sequence   
    39 {
    40 public:
    41     //将元素添加到堆栈的顶部。
    42     void push(int x) override
    43     {
    44         m_deque.push_front(x);
    45     }
    46     //从堆栈中删除顶部元素
    47     void pop() override
    48     {
    49         m_deque.pop_front();
    50     }
    51 private:
    52     Deque m_deque;
    53 };
    54 ​
    55 //队列，先进先出，适配类
    56 class Queue:public Sequence  
    57 {
    58 public:
    59     //将元素添加到队列尾部
    60     void push(int x) override
    61     {
    62         m_deque.push_back(x);
    63     }
    64     //从队列中删除顶部元素
    65     void pop() override
    66     {
    67         m_deque.pop_front();
    68     }
    69 private:
    70     Deque m_deque;
    71 };
    
     

## 3.2、使用继承实现适配器模式

    
     1 //双端队列，被适配类
     2 class Deque  
     3 {
     4 public:
     5     void push_back(int x)
     6     {
     7         cout << "Deque push_back:" << x << endl;
     8     }
     9     void push_front(int x)
    10     {
    11         cout << "Deque push_front:" << x << endl;
    12     }
    13     void pop_back()
    14     {
    15         cout << "Deque pop_back" << endl;
    16     }
    17     void pop_front()
    18     {
    19         cout << "Deque pop_front" << endl;
    20     }
    21 };
    22 ​
    23 //顺序类，抽象目标类
    24 class Sequence  
    25 {
    26 public:
    27     virtual void push(int x) = 0;
    28     virtual void pop() = 0;
    29 };
    30 ​
    31 //栈,后进先出, 适配类
    32 class Stack:public Sequence, private Deque   
    33 {
    34 public:
    35     void push(int x)
    36     {
    37         push_front(x);
    38     }
    39     void pop()
    40     {
    41         pop_front();
    42     }
    43 };
    44 ​
    45 //队列，先进先出，适配类
    46 class Queue:public Sequence, private Deque 
    47 {
    48 public:
    49     void push(int x)
    50     {
    51         push_back(x);
    52     }
    53     void pop()
    54     {
    55         pop_front();
    56     }
    57 };
   
## 7、建造者模式

建造者模式：将复杂对象的构建和其表示分离，使得相同的构建过程可以产生不同的表示。

以下情形可以考虑使用建造者模式：

对象的创建复杂，但是其各个部分的子对象创建算法一定。

需求变化大，构造复杂对象的子对象经常变化，但将其组合在一起的算法相对稳定。

建造者模式的优点：

将对象的创建和表示分离，客户端不需要了解具体的构建细节。

增加新的产品对象时，只需要增加其具体的建造类即可，不需要修改原来的代码，扩展方便。

产品之间差异性大，内部变化较大、较复杂时不建议使用建造者模式。

    复制代码
      1 /*
      2 *关键代码：建造者类：创建和提供实例； Director类：管理建造出来的实例的依赖关系。
      3 */
      4 ​
      5 #include <iostream>
      6 #include <string>
      7 ​
      8 using namespace std;
      9 ​
     10 //具体的产品类
     11 class Order
     12 {
     13 public:
     14     void setFood(const string& food)
     15     {
     16         m_strFood = food;
     17     }
     18 ​
     19     const string& food()
     20     {
     21         cout << m_strFood.data() << endl;
     22         return m_strFood;
     23     }
     24     
     25     void setDrink(const string& drink)
     26     {
     27         m_strDrink = drink;
     28     }
     29 ​
     30     const string& drink()
     31     {
     32         cout << m_strDrink << endl;
     33         return m_strDrink;
     34     }
     35 ​
     36 private:
     37     string m_strFood;
     38     string m_strDrink;
     39 };
     40 ​
     41 //抽象建造类，提供建造接口。
     42 class OrderBuilder
     43 {
     44 public:
     45     virtual ~OrderBuilder()
     46     {
     47         cout << "~OrderBuilder()" << endl;
     48     }
     49     virtual void setOrderFood() = 0;
     50     virtual void setOrderDrink() = 0;
     51     virtual Order* getOrder() = 0;
     52 };
     53 ​
     54 //具体的建造类
     55 class VegetarianOrderBuilder : public OrderBuilder 
     56 {
     57 public:
     58     VegetarianOrderBuilder()
     59     {
     60         m_pOrder = new Order;
     61     }
     62 ​
     63     ~VegetarianOrderBuilder()
     64     {
     65         cout << "~VegetarianOrderBuilder()" << endl;
     66         delete m_pOrder;
     67         m_pOrder = nullptr;
     68     }
     69 ​
     70     void setOrderFood() override
     71     {
     72         m_pOrder->setFood("vegetable salad");
     73     }
     74 ​
     75     void setOrderDrink() override
     76     {
     77         m_pOrder->setDrink("water");
     78     }
     79 ​
     80     Order* getOrder() override
     81     {
     82         return m_pOrder;
     83     }
     84 ​
     85 private:
     86     Order* m_pOrder;
     87 };
     88 ​
     89 //具体的建造类
     90 class MeatOrderBuilder : public OrderBuilder
     91 {
     92 public:
     93     MeatOrderBuilder()
     94     {
     95         m_pOrder = new Order;
     96     }
     97     ~MeatOrderBuilder()
     98     {
     99         cout << "~MeatOrderBuilder()" << endl;
    100         delete m_pOrder;
    101         m_pOrder = nullptr;
    102     }
    103 ​
    104     void setOrderFood() override
    105     {
    106         m_pOrder->setFood("beef");
    107     }
    108 ​
    109     void setOrderDrink() override
    110     {
    111         m_pOrder->setDrink("beer");
    112     }
    113 ​
    114     Order* getOrder() override
    115     {
    116         return m_pOrder;
    117     }
    118 ​
    119 private:
    120     Order* m_pOrder;
    121 };
    122 ​
    123 //Director类，负责管理实例创建的依赖关系，指挥构建者类创建实例
    124 class Director
    125 {
    126 public:
    127     Director(OrderBuilder* builder) : m_pOrderBuilder(builder)
    128     {
    129     }
    130     void construct()
    131     {
    132         m_pOrderBuilder->setOrderFood();
    133         m_pOrderBuilder->setOrderDrink();
    134     }
    135 ​
    136 private:
    137     OrderBuilder* m_pOrderBuilder;
    138 };
    139 ​
    140 ​
    141 int main()
    142 {
    143 //  MeatOrderBuilder* mBuilder = new MeatOrderBuilder;
    144     OrderBuilder* mBuilder = new MeatOrderBuilder;  //注意抽象构建类必须有虚析构函数，解析时才会                                                      调用子类的析构函数
    145     Director* director = new Director(mBuilder);
    146     director->construct();
    147 Order* order = mBuilder->getOrder();
    148 order->food();
    149 order->drink();
    150 ​
    151 delete director;
    152 director = nullptr;
    153 ​
    154 delete mBuilder;
    155 mBuilder = nullptr;
    156 ​
    157 return 0;
    158 }
    复制代码

 

## 8、外观模式

外观模式：为子系统中的一组接口定义一个一致的界面；外观模式提供一个高层的接口，这个接口使得这一子系统更加容易被使用；对于复杂的系统，系统为客户端提供一个简单的接口，把负责的实现过程封装起来，客户端不需要连接系统内部的细节。

以下情形建议考虑外观模式：

设计初期阶段，应有意识的将不同层分离，层与层之间建立外观模式。

开发阶段，子系统越来越复杂，使用外观模式提供一个简单的调用接口。

一个系统可能已经非常难易维护和扩展，但又包含了非常重要的功能，可以为其开发一个外观类，使得新系统可以方便的与其交互。

优点：

实现了子系统与客户端之间的松耦合关系。

客户端屏蔽了子系统组件，减少了客户端所需要处理的对象数据，使得子系统使用起来更方便容易。

更好的划分了设计层次，对于后期维护更加的容易。

    复制代码
     1 /*
     2 * 关键代码：客户与系统之间加一个外观层，外观层处理系统的调用关系、依赖关系等。
     3 *以下实例以电脑的启动过程为例，客户端只关心电脑开机的、关机的过程，并不需要了解电脑内部子系统的启动过程。
     4 */
     5 #include <iostream>
     6 ​
     7 using namespace std;
     8 ​
     9 //抽象控件类，提供接口
    10 class Control
    11 {
    12 public:
    13     virtual void start() = 0;
    14     virtual void shutdown() = 0;
    15 };
    16 ​
    17 //子控件， 主机
    18 class Host : public Control
    19 {
    20 public:
    21     void start() override
    22     {
    23         cout << "Host start" << endl;
    24     }
    25     void shutdown() override
    26     {
    27         cout << "Host shutdown" << endl;
    28     }
    29 };
    30 ​
    31 //子控件， 显示屏
    32 class LCDDisplay : public Control
    33 {
    34 public:
    35     void start() override
    36     {
    37         cout << "LCD Display start" << endl;
    38     }
    39     void shutdown() override
    40     {
    41         cout << "LCD Display shutdonw" << endl;
    42     }
    43 };
    44 ​
    45 //子控件， 外部设备
    46 class Peripheral : public Control
    47 {
    48 public:
    49     void start() override
    50     {
    51         cout << "Peripheral start" << endl;
    52     }
    53     void shutdown() override
    54     {
    55         cout << "Peripheral shutdown" << endl;
    56     }
    57 };
    58 ​
    59 class Computer
    60 {
    61 public:
    62     void start()
    63     {
    64         m_host.start();
    65         m_display.start();
    66         m_peripheral.start();
    67         cout << "Computer start" << endl;
    68     }
    69     void shutdown()
    70     {
    71         m_host.shutdown();
    72         m_display.shutdown();
    73         m_peripheral.shutdown();
    74         cout << "Computer shutdown" << endl;
    75     }
    76 private:
    77     Host   m_host;
    78     LCDDisplay m_display;
    79     Peripheral   m_peripheral;
    80 };
    81 ​
    82 int main()
    83 {
    84     Computer computer;
    85     computer.start();
    86 ​
    87     //do something
    88 ​
    89     computer.shutdown();
    90 ​
    91     return 0;
    92 }
    复制代码

 

## 9、组合模式

组合模式：将对象组合成树形结构以表示“部分-整体”的层次结构，组合模式使得客户端对单个对象和组合对象的使用具有一直性。

既然讲到以树形结构表示“部分-整体”，那可以将组合模式想象成一根大树，将大树分成树枝和树叶两部分，树枝上可以再长树枝，也可以长树叶，树叶上则不能再长出别的东西。

以下情况可以考虑使用组合模式：

希望表示对象的部分-整体层次结构。

希望客户端忽略组合对象与单个对象的不同，客户端将统一的使用组合结构中的所有对象。

    复制代码
      1 /*
      2 * 关键代码：树枝内部组合该接口，并且含有内部属性list，里面放Component。
      3 */
      4 
      5 #include <iostream>
      6 #include <list>
      7 #include <memory>
      8 
      9 using namespace std;
     10 
     11 //抽象类，提供组合和单个对象的一致接口
     12 class Company
     13 {
     14 public:
     15     Company(const string& name): m_name(name){}
     16     virtual ~Company(){ cout << "~Company()" << endl;}
     17 
     18     virtual void add(Company* ) = 0;
     19     virtual void remove(const string&) = 0;
     20     virtual void display(int depth) = 0;
     21 
     22     virtual const string& name()
     23     {
     24         return m_name;
     25     }
     26 
     27 protected:
     28     string m_name;
     29 };
     30 
     31 //具体的单个对象实现类，“树枝”类
     32 class HeadCompany : public Company
     33 {
     34 public:
     35     HeadCompany(const string& name): Company(name){}
     36     virtual ~HeadCompany(){ cout << "~HeadCompany()" << endl;}
     37 
     38     void add(Company* company) override
     39     {
     40         shared_ptr<Company> temp(company);
     41         m_companyList.push_back(temp);
     42     }
     43 
     44     void remove(const string& strName) override
     45     {
     46         list<shared_ptr<Company>>::iterator iter = m_companyList.begin();
     47         for(; iter != m_companyList.end(); iter++)
     48         {
     49             if((*iter).get()->name() == strName)
     50             {
     51             //不应该在此处使用list<T>.erase(list<T>::iterator iter),会导致iter++错误，这里删除目               标元素之后，必须return。
     52                 m_companyList.erase(iter);
     53                 return;
     54             }
     55         }
     56     }
     57 
     58     void display(int depth) override
     59     {
     60         for(int i = 0; i < depth; i++)
     61         {
     62             cout << "-";
     63         }
     64         cout << this->name().data() << endl;
     65         list<shared_ptr<Company>>::iterator iter = m_companyList.begin();
     66         for(; iter!= m_companyList.end(); iter++)
     67         {
     68             (*iter).get()->display(depth + 1);
     69         }
     70     }
     71 
     72 private:
     73     list<shared_ptr<Company>> m_companyList;
     74 };
     75 
     76 //具体的单个对象实现类，“树叶”类
     77 class ResearchCompany : public Company
     78 {
     79 public:
     80     ResearchCompany(const string& name): Company(name){}
     81     virtual ~ResearchCompany(){ cout << "~ResearchCompany()" << endl;}
     82 
     83     void add(Company* ) override
     84     {
     85     }
     86 
     87     void remove(const string&) override
     88     {
     89     }
     90 
     91     void display(int depth) override
     92     {
     93         for(int i = 0; i < depth; i++)
     94         {
     95             cout << "-";
     96         }
     97         cout << m_name.data() << endl;
     98     }
     99 };
    100 
    101 //具体的单个对象实现类，“树叶”类
    102 class SalesCompany : public Company
    103 {
    104 public:
    105     SalesCompany(const string& name): Company(name){}
    106     virtual ~SalesCompany(){ cout << "~SalesCompany()" << endl;}
    107 
    108     void add(Company* ) override
    109     {
    110     }
    111 
    112     void remove(const string&) override
    113     {
    114     }
    115 
    116     void display(int depth) override
    117     {
    118         for(int i = 0; i < depth; i++)
    119         {
    120             cout << "-";
    121         }
    122         cout << m_name.data() << endl;
    123     }
    124 };
    125 
    126 //具体的单个对象实现类，“树叶”类
    127 class FinanceCompany : public Company
    128 {
    129 public:
    130     FinanceCompany(const string& name): Company(name){}
    131     virtual ~FinanceCompany(){ cout << "~FinanceCompany()" << endl;}
    132 
    133     void add(Company* ) override
    134     {
    135     }
    136 
    137     void remove(const string&) override
    138     {
    139     }
    140 
    141     void display(int depth) override
    142     {
    143         for(int i = 0; i < depth; i++)
    144         {
    145             cout << "-";
    146         }
    147         cout << m_name.data() << endl;
    148     }
    149 };
    150 
    151 
    152 int main()
    153 {
    154     HeadCompany* headRoot = new HeadCompany("Head Root Company");
    155 
    156     HeadCompany* childRoot1 = new HeadCompany("Child Company A");
    157     ResearchCompany* r1 = new ResearchCompany("Research Company A");
    158     SalesCompany* s1 = new SalesCompany("Sales Company A");
    159     SalesCompany* s2 = new SalesCompany("Sales Company B");
    160     FinanceCompany* f1 = new FinanceCompany("FinanceCompany A");
    161     
    162     childRoot1->add(r1);
    163     childRoot1->add(s1);
    164     childRoot1->add(s2);
    165     childRoot1->add(f1);
    166 
    167     HeadCompany* childRoot2 = new HeadCompany("Child Company B");
    168     ResearchCompany* r2 = new ResearchCompany("Research Company B");
    169     SalesCompany* s3 = new SalesCompany("Sales Company C");
    170     SalesCompany* s4 = new SalesCompany("Sales Company D");
    171     FinanceCompany* f2 = new FinanceCompany("FinanceCompany B");
    172     
    173     childRoot2->add(r2);
    174     childRoot2->add(s3);
    175     childRoot2->add(s4);
    176     childRoot2->add(f2);
    177 
    178     headRoot->add(childRoot1);
    179     headRoot->add(childRoot2);
    180     headRoot->display(1);
    181     
    182     cout << "\n***************\n" << endl;
    183 
    184     childRoot1->remove("Sales Company B");
    185     headRoot->display(1);
    186     
    187     cout << "\n***************\n" << endl;
    188 
    189     delete headRoot;
    190     headRoot = nullptr;
    191 
    192     return 0;
    193 }
    复制代码

 

## 10、代理模式

代理模式：为其它对象提供一种代理以控制这个对象的访问。在某些情况下，一个对象不适合或者不能直接引用另一个对象，而代理对象可以在客户端和目标对象之间起到中介作用。

优点：

职责清晰。真实的角色只负责实现实际的业务逻辑，不用关心其它非本职责的事务，通过后期的代理完成具体的任务。这样代码会简洁清晰。

代理对象可以在客户端和目标对象之间起到中介的作用，这样就保护了目标对象。

扩展性好。

    复制代码
     1 /*
     2 * 关键代码：一个是真正的你要访问的对象(目标类)，一个是代理对象,真正对象与代理对象实现同一个接口,先访问代理*         类再访问真正要访问的对象。
     3 */
     4 #include <iostream>
     5 ​
     6 using namespace std;
     7 ​
     8 class Gril
     9 {
    10 public:
    11     Gril(const string& name = "gril"):m_string(name){}
    12     string getName()
    13     {
    14         return m_string;
    15     }
    16 private:
    17     string m_string;
    18 };
    19 ​
    20 class Profession
    21 {
    22 public:
    23     virtual ~Profession(){}
    24     virtual void profess() = 0;
    25 };
    26 ​
    27 class YoungMan : public Profession
    28 {
    29 public:
    30     YoungMan(const Gril& gril):m_gril(gril){}
    31     void profess()
    32     {
    33         cout << "Young man love " << m_gril.getName().data() << endl;
    34     }
    35 ​
    36 private:
    37     Gril m_gril;
    38 };
    39 ​
    40 class ManProxy : public Profession
    41 {
    42 public:
    43     ManProxy(const Gril& gril):m_pMan(new YoungMan(gril)){}
    44     ~ManProxy()
    45     {
    46         delete m_pMan;
    47         m_pMan = nullptr;
    48     }
    49     void profess()
    50     {
    51         m_pMan->profess();
    52     }
    53 private:
    54     YoungMan* m_pMan;
    55 };
    56 ​
    57 int main(int argc, char *argv[])
    58 {
    59     Gril gril("heihei");
    60     ManProxy* proxy = new ManProxy(gril);
    61     proxy->profess();
    62 ​
    63     delete proxy;
    64     proxy = nullptr;
    65     return 0;
    66 }
    复制代码

 

## 11、享元模式

享元模式：运用共享技术有效地支持大量细粒度的对象。在有大量对象时，把其中共同的部分抽象出来，如果有相同的业务请求，直接返回内存中已有的对象，避免重新创建。

以下情况可以考虑使用享元模式：

系统中有大量的对象，这些对象消耗大量的内存，且这些对象的状态可以被外部化。

对于享元模式，需要将对象的信息分为两个部分：内部状态和外部状态。内部状态是指被共享出来的信息，储存在享元对象内部且不随环境变化而改变；外部状态是不可以共享的，它随环境改变而改变，是由客户端控制的。

    复制代码
      1 /*
      2 * 关键代码：将内部状态作为标识，进行共享。
      3 */
      4 #include <iostream>
      5 #include <map>
      6 #include <memory>
      7 ​
      8 using namespace std;
      9 ​
     10 //抽象享元类，提供享元类外部接口。
     11 class AbstractConsumer
     12 {
     13 public:
     14     virtual ~AbstractConsumer(){}
     15     virtual void setArticle(const string&) = 0;
     16     virtual const string& article() = 0;
     17 };
     18 ​
     19 //具体的享元类
     20 class Consumer : public AbstractConsumer
     21 {
     22 public:
     23     Consumer(const string& strName) : m_user(strName){}
     24     ~Consumer()
     25     {
     26         cout << " ~Consumer()" << endl;
     27     }
     28 ​
     29     void setArticle(const string& info) override
     30     {
     31         m_article = info;
     32     }
     33 ​
     34     const string& article() override
     35     {
     36         return m_article;
     37     }
     38 ​
     39 private:
     40     string m_user;
     41     string m_article;
     42 };
     43 ​
     44 //享元工厂类
     45 class Trusteeship
     46 {
     47 public:
     48     ~Trusteeship()
     49     {
     50          m_consumerMap.clear();
     51     }
     52 ​
     53     void hosting(const string& user, const string& article)
     54     {
     55         if(m_consumerMap.count(user))
     56         {
     57             cout << "A customer named " << user.data() << " already exists" << endl;
     58             Consumer* consumer = m_consumerMap.at(user).get();
     59             consumer->setArticle(article);
     60         }
     61         else
     62         {
     63             shared_ptr<Consumer> consumer(new Consumer(user));
     64             consumer.get()->setArticle(article);
     65             m_consumerMap.insert(pair<string, shared_ptr<Consumer>>(user, consumer));
     66         }
     67     }
     68 ​
     69     void display()
     70     {
     71         map<string, shared_ptr<Consumer>>::iterator iter = m_consumerMap.begin();
     72         for(; iter != m_consumerMap.end(); iter++)
     73         {
     74             cout << iter->first.data() << " : "<< iter->second.get()->article().data() << endl;
     75         }
     76     }
     77 ​
     78 private:
     79     map<string, shared_ptr<Consumer>> m_consumerMap;
     80 };
     81 ​
     82 ​
     83 int main()
     84 {
     85     Trusteeship* ts = new Trusteeship;
     86     ts->hosting("zhangsan", "computer");
     87     ts->hosting("lisi", "phone");
     88     ts->hosting("wangwu", "watch");
     89 ​
     90     ts->display();
     91 ​
     92     ts->hosting("zhangsan", "TT");
     93     ts->hosting("lisi", "TT");
     94     ts->hosting("wangwu", "TT");
     95 ​
     96     ts->display();
     97 ​
     98     delete ts;
     99     ts = nullptr;
    100 ​
    101     return 0;
    102 }
    复制代码
     

## 12、桥接模式

桥接模式：将抽象部分与实现部分分离，使它们都可以独立变换。

以下情形考虑使用桥接模式：

当一个对象有多个变化因素的时候，考虑依赖于抽象的实现，而不是具体的实现。

当多个变化因素在多个对象间共享时，考虑将这部分变化的部分抽象出来再聚合/合成进来。

当一个对象的多个变化因素可以动态变化的时候。

优点：

将实现抽离出来，再实现抽象，使得对象的具体实现依赖于抽象，满足了依赖倒转原则。

更好的可扩展性。

可动态的切换实现。桥接模式实现了抽象和实现的分离，在实现桥接模式时，就可以实现动态的选择具体的实现。

    复制代码
     1 /*
     2 * 关键代码：将现实独立出来，抽象类依赖现实类。
     3 * 以下示例中，将各类App、各类手机独立开来，实现各种App和各种手机的自由桥接。
     4 */
     5 #include <iostream>
     6 ​
     7 using namespace std;
     8 ​
     9 //抽象App类，提供接口
    10 class App
    11 {
    12 public:
    13     virtual ~App(){ cout << "~App()" << endl; }
    14     virtual void run() = 0;
    15 };
    16 ​
    17 //具体的App实现类
    18 class GameApp:public App
    19 {
    20 public:
    21     void run()
    22     {
    23         cout << "GameApp Running" << endl;
    24     }
    25 };
    26 ​
    27 //具体的App实现类
    28 class TranslateApp:public App
    29 {
    30 public:
    31     void run()
    32     {
    33         cout << "TranslateApp Running" << endl;
    34     }
    35 };
    36 ​
    37 //抽象手机类，提供接口
    38 class MobilePhone
    39 {
    40 public:
    41     virtual ~MobilePhone(){ cout << "~MobilePhone()" << endl;}
    42     virtual void appRun(App* app) = 0;  //实现App与手机的桥接
    43 };
    44 ​
    45 //具体的手机实现类
    46 class XiaoMi:public MobilePhone
    47 {
    48 public:
    49     void appRun(App* app)
    50     {
    51         cout << "XiaoMi: ";
    52         app->run();
    53     }
    54 };
    55 ​
    56 //具体的手机实现类
    57 class HuaWei:public MobilePhone
    58 {
    59 public:
    60     void appRun(App* app)
    61     {
    62         cout << "HuaWei: ";
    63         app->run();
    64     }
    65 };
    66 ​
    67 int main()
    68 {
    69     App* gameApp = new GameApp;
    70     App* translateApp = new TranslateApp;
    71     MobilePhone* mi = new XiaoMi;
    72     MobilePhone* hua = new HuaWei;
    73     mi->appRun(gameApp);
    74     mi->appRun(translateApp);
    75     hua->appRun(gameApp);
    76     hua->appRun(translateApp);
    77 ​
    78     delete hua;
    79     hua = nullptr;
    80     delete mi;
    81     mi = nullptr;
    82     delete gameApp;
    83     gameApp = nullptr;
    84     delete translateApp;
    85     translateApp = nullptr;
    86 ​
    87     return 0;
    88 }
    复制代码
     

## 13、装饰模式

装饰模式：动态地给一个对象添加一些额外的功能，它是通过创建一个包装对象，也就是装饰来包裹真实的对象。新增加功能来说，装饰器模式比生产子类更加灵活。

以下情形考虑使用装饰模式：

需要扩展一个类的功能，或给一个类添加附加职责。

需要动态的给一个对象添加功能，这些功能可以再动态的撤销。

需要增加由一些基本功能的排列组合而产生的非常大量的功能，从而使继承关系变的不现实。

当不能采用生成子类的方法进行扩充时。一种情况是，可能有大量独立的扩展，为支持每一种组合将产生大量的子类，使得子类数目呈爆炸性增长。另一种情况可能是因为类定义被隐藏，或类定义不能用于生成子类。

    复制代码
      1 /*
      2 * 关键代码：1、Component 类充当抽象角色，不应该具体实现。 2、修饰类引用和继承 Component 类，具体扩展类重写父类方法。
      3 */
      4 #include <iostream>
      5 ​
      6 using namespace std;
      7 ​
      8 //抽象构件（Component）角色：给出一个抽象接口，以规范准备接收附加责任的对象。
      9 class Component
     10 {
     11 public:
     12     virtual ~Component(){}
     13 ​
     14     virtual void configuration() = 0;
     15 };
     16 ​
     17 //具体构件（Concrete Component）角色：定义一个将要接收附加责任的类。
     18 class Car : public Component
     19 {
     20 public:
     21     void configuration() override
     22     {
     23         cout << "A Car" << endl;
     24     }
     25 };
     26 ​
     27 //装饰（Decorator）角色：持有一个构件（Component）对象的实例，并实现一个与抽象构件接口一致的接口。
     28 class DecorateCar : public Component
     29 {
     30 public:
     31     DecorateCar(Component* car) : m_pCar(car){}
     32 ​
     33     void configuration() override
     34     {
     35         m_pCar->configuration();
     36     }
     37 ​
     38 private:
     39     Component* m_pCar;
     40 };
     41 ​
     42 //具体装饰（Concrete Decorator）角色：负责给构件对象添加上附加的责任。
     43 class DecorateLED : public DecorateCar
     44 {
     45 public:
     46     DecorateLED(Component* car) : DecorateCar(car){}
     47 ​
     48     void configuration() override
     49     {
     50         DecorateCar::configuration();
     51         addLED();
     52     }
     53 ​
     54 private:
     55     void addLED()
     56     {
     57         cout << "Install LED" << endl;
     58     }
     59 ​
     60 };
     61 ​
     62 //具体装饰（Concrete Decorator）角色：负责给构件对象添加上附加的责任。
     63 class DecoratePC : public DecorateCar
     64 {
     65 public:
     66     DecoratePC(Component* car) : DecorateCar(car){}
     67 ​
     68     void configuration() override
     69     {
     70         DecorateCar::configuration();
     71         addPC();
     72     }
     73 ​
     74 private:
     75     void addPC()
     76     {
     77         cout << "Install PC" << endl;
     78     }
     79 };
     80 ​
     81 //具体装饰（Concrete Decorator）角色：负责给构件对象添加上附加的责任。
     82 class DecorateEPB : public DecorateCar
     83 {
     84 public:
     85     DecorateEPB(Component* car) : DecorateCar(car){}
     86 ​
     87     void configuration() override
     88     {
     89         DecorateCar::configuration();
     90         addEPB();
     91     }
     92 ​
     93 private:
     94     void addEPB()
     95     {
     96         cout << "Install Electrical Park Brake" << endl;
     97     }
     98 };
     99 ​
    100 int main()
    101 {
    102     Car* car = new Car;
    103     DecorateLED* ledCar = new DecorateLED(car);
    104     DecoratePC* pcCar = new DecoratePC(ledCar);
    105     DecorateEPB* epbCar = new DecorateEPB(pcCar);
    106 ​
    107     epbCar->configuration();
    108 ​
    109     delete epbCar;
    110     epbCar = nullptr;
    111 ​
    112     delete pcCar;
    113     pcCar = nullptr;
    114 ​
    115     delete ledCar;
    116     ledCar = nullptr;
    117 ​
    118     delete car;
    119     car = nullptr;
    120 ​
    121     return 0;
    122 }
    复制代码
     

## 14、备忘录模式

备忘录模式：在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。这样以后就可以将该对象恢复到原来保存的状态。

备忘录模式中需要定义的角色类：

Originator(发起人)：负责创建一个备忘录Memento，用以记录当前时刻自身的内部状态，并可使用备忘录恢复内部状态。Originator可以根据需要决定Memento存储自己的哪些内部状态。

Memento(备忘录)：负责存储Originator对象的内部状态，并可以防止Originator以外的其他对象访问备忘录。备忘录有两个接口：Caretaker只能看到备忘录的窄接口，他只能将备忘录传递给其他对象。Originator却可看到备忘录的宽接口，允许它访问返回到先前状态所需要的所有数据。

Caretaker(管理者):负责备忘录Memento，不能对Memento的内容进行访问或者操作。

    复制代码
      1 /*
      2 * 关键代码：Memento类、Originator类、Caretaker类；Originator类不与Memento类耦合，而是与Caretaker类耦合。
      3 */
      4 ​
      5 include <iostream>
      6 ​
      7 using namespace std;
      8 ​
      9 //需要保存的信息
     10 typedef struct  
     11 {
     12     int grade;
     13     string arm;
     14     string corps;
     15 }GameValue;
     16 ​
     17 //Memento类
     18 class Memento   
     19 {
     20 public:
     21     Memento(){}
     22     Memento(GameValue value):m_gameValue(value){}
     23     GameValue getValue()
     24     {
     25         return m_gameValue;
     26     }
     27 private:
     28     GameValue m_gameValue;
     29 };
     30 ​
     31 //Originator类
     32 class Game   
     33 {
     34 public:
     35     Game(GameValue value):m_gameValue(value)
     36     {}
     37     void addGrade()  //等级增加
     38     {
     39         m_gameValue.grade++;
     40     }
     41     void replaceArm(string arm)  //更换武器
     42     {
     43         m_gameValue.arm = arm;
     44     }
     45     void replaceCorps(string corps)  //更换工会
     46     {
     47         m_gameValue.corps = corps;
     48     }
     49     Memento saveValue()    //保存当前信息
     50     {
     51         Memento memento(m_gameValue);
     52         return memento;
     53     }
     54     void load(Memento memento) //载入信息
     55     {
     56         m_gameValue = memento.getValue();
     57     }
     58     void showValue()
     59     {
     60         cout << "Grade: " << m_gameValue.grade << endl;
     61         cout << "Arm  : " << m_gameValue.arm.data() << endl;
     62         cout << "Corps: " << m_gameValue.corps.data() << endl;
     63     }
     64 private:
     65     GameValue m_gameValue;
     66 };
     67 ​
     68 //Caretaker类
     69 class Caretake 
     70 {
     71 public:
     72     void save(Memento memento)  //保存信息
     73     {
     74         m_memento = memento;
     75     }
     76     Memento load()            //读已保存的信息
     77     {
     78         return m_memento;
     79     }
     80 private:
     81     Memento m_memento;
     82 };
     83 ​
     84 int main()
     85 {
     86     GameValue v1 = {0, "Ak", "3K"};
     87     Game game(v1);    //初始值
     88     game.addGrade();
     89     game.showValue();
     90     cout << "----------" << endl;
     91     Caretake care;
     92     care.save(game.saveValue());  //保存当前值
     93     game.addGrade();          //修改当前值
     94     game.replaceArm("M16");
     95     game.replaceCorps("123");
     96     game.showValue();
     97     cout << "----------" << endl;
     98     game.load(care.load());   //恢复初始值
     99     game.showValue();
    100     return 0;
    101 }
    复制代码

 

## 15、中介者模式

中介者模式：用一个中介对象来封装一系列的对象交互，中介者使各对象不需要显示地相互引用，从而使其耦合松散，而且可以独立地改变它们之前的交互。

如果对象与对象之前存在大量的关联关系，若一个对象改变，常常需要跟踪与之关联的对象，并做出相应的处理，这样势必会造成系统变得复杂，遇到这种情形可以考虑使用中介者模式。当多个对象存在关联关系时，为它们设计一个中介对象，当一个对象改变时，只需要通知它的中介对象，再由它的中介对象通知每个与它相关的对象。

    复制代码
      1 /*
      2 * 关键代码：将相关对象的通信封装到一个类中单独处理。
      3 */
      4 #include <iostream>
      5 ​
      6 using namespace std;
      7 ​
      8 class Mediator;
      9 ​
     10 //抽象同事类。
     11 class Businessman
     12 {
     13 public:
     14     Businessman(){}
     15     Businessman(Mediator* mediator) : m_pMediator(mediator){}
     16 ​
     17     virtual ~Businessman(){}
     18 ​
     19     virtual void setMediator(Mediator* m)
     20     {
     21         m_pMediator = m;
     22     }
     23 ​
     24     virtual void sendMessage(const string& msg) = 0;
     25     virtual void getMessage(const string& msg) = 0;
     26 ​
     27 protected:
     28     Mediator* m_pMediator;
     29 };
     30 ​
     31 //抽象中介者类。
     32 class  Mediator
     33 {
     34 public:
     35     virtual ~Mediator(){}
     36     virtual void setBuyer(Businessman* buyer) = 0;
     37     virtual void setSeller(Businessman* seller) = 0;
     38     virtual void send(const string& msg, Businessman* man) = 0;
     39 };
     40 ​
     41 //具体同事类
     42 class Buyer : public Businessman
     43 {
     44 public:
     45     Buyer() : Businessman(){}
     46     Buyer(Mediator* mediator) : Businessman(mediator){}
     47 ​
     48     void sendMessage(const string& msg) override
     49     {
     50         m_pMediator->send(msg, this);
     51     }
     52 ​
     53     void getMessage(const string& msg)
     54     {
     55         cout << "Buyer recv: " << msg.data() << endl;
     56     }
     57 };
     58 ​
     59 //具体同事类
     60 class Seller : public Businessman
     61 {
     62 public:
     63     Seller() : Businessman(){}
     64     Seller(Mediator* mediator) : Businessman(mediator){}
     65 ​
     66     void sendMessage(const string& msg) override
     67     {
     68         m_pMediator->send(msg, this);
     69     }
     70 ​
     71     void getMessage(const string& msg)
     72     {
     73         cout << "Seller recv: " << msg.data() << endl;
     74     }
     75 };
     76 ​
     77 //具体中介者类
     78 class HouseMediator : public Mediator
     79 {
     80 public:
     81     void setBuyer(Businessman* buyer) override
     82     {
     83         m_pBuyer = buyer;
     84     }
     85 ​
     86     void setSeller(Businessman* seller) override
     87     {
     88         m_pSeller = seller;
     89     }
     90 ​
     91     void send(const string& msg, Businessman* man) override
     92     {
     93         if(man == m_pBuyer)
     94         {
     95             m_pSeller->getMessage(msg);
     96         }
     97         else if(man == m_pSeller)
     98         {
     99             m_pBuyer->getMessage(msg);
    100         }
    101     }
    102 ​
    103 private:
    104     Businessman* m_pBuyer;
    105     Businessman* m_pSeller;
    106 };
    107 ​
    108 int main()
    109 {
    110     HouseMediator* hMediator = new HouseMediator;
    111     Buyer* buyer = new Buyer(hMediator);
    112     Seller* seller = new Seller(hMediator);
    113 ​
    114     hMediator->setBuyer(buyer);
    115     hMediator->setSeller(seller);
    116 ​
    117     buyer->sendMessage("Sell not to sell?");
    118     seller->sendMessage("Of course selling!");
    119 ​
    120     delete buyer;
    121     buyer = nullptr;
    122 ​
    123     delete seller;
    124     seller = nullptr;
    125 ​
    126     delete hMediator;
    127     hMediator = nullptr;
    128 ​
    129 ​
    130     return 0;
    131 }
    复制代码

 

## 16、职责链模式

职责链模式：使多个对象都有机会处理请求，从而避免请求的发送者和接收者之前的耦合关系，将这些对象连成一条链，并沿着这条链传递请求，直到有一个对象处理它为止。

职责链上的处理者负责处理请求，客户只需要将请求发送到职责链上即可，无需关心请求的处理细节和请求的传递，所有职责链将请求的发送者和请求的处理者解耦了。

    复制代码
     1 /*
     2 * 关键代码：Handler内指明其上级，handleRequest()里判断是否合适，不合适则传递给上级。
     3 */
     4 #include <iostream>
     5 ​
     6 using namespace std;
     7 ​
     8 enum RequestLevel
     9 {
    10     Level_One = 0,
    11     Level_Two,
    12     Level_Three,
    13     Level_Num
    14 };
    15 ​
    16 //抽象处理者（Handler）角色，提供职责链的统一接口。
    17 class Leader
    18 {
    19 public:
    20     Leader(Leader* leader):m_leader(leader){}
    21     virtual ~Leader(){}
    22     virtual void handleRequest(RequestLevel level) = 0;
    23 protected:
    24     Leader* m_leader;
    25 };
    26 ​
    27 //具体处理者（Concrete Handler）角色
    28 class Monitor:public Leader   //链扣1
    29 {
    30 public:
    31     Monitor(Leader* leader):Leader(leader){}
    32     void handleRequest(RequestLevel level)
    33     {
    34         if(level < Level_Two)
    35         {
    36             cout << "Mointor handle request : " << level << endl;
    37         }
    38         else
    39         {
    40             m_leader->handleRequest(level);
    41         }
    42     }
    43 };
    44 ​
    45 //具体处理者（Concrete Handler）角色
    46 class Captain:public Leader    //链扣2
    47 {
    48 public:
    49     Captain(Leader* leader):Leader(leader){}
    50     void handleRequest(RequestLevel level)
    51     {
    52         if(level < Level_Three)
    53         {
    54             cout << "Captain handle request : " << level << endl;
    55         }
    56         else
    57         {
    58             m_leader->handleRequest(level);
    59         }
    60     }
    61 };
    62 ​
    63 //具体处理者（Concrete Handler）角色
    64 class General:public Leader   //链扣3
    65 {
    66 public:
    67     General(Leader* leader):Leader(leader){}
    68     void handleRequest(RequestLevel level)
    69     {
    70         cout << "General handle request : " << level << endl;
    71     }
    72 };
    73 ​
    74 int main()
    75 {
    76     Leader* general = new General(nullptr);
    77     Leader* captain = new Captain(general);
    78     Leader* monitor = new Monitor(captain);
    79     monitor->handleRequest(Level_One);
    80 ​
    81     delete monitor;
    82     monitor = nullptr;
    83     delete captain;
    84     captain = nullptr;
    85     delete general;
    86     general = nullptr;
    87     return 0;
    88 }
    复制代码

 

## 17、观察者模式

观察者模式：定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都要得到通知并自动更新。

观察者模式从根本上讲必须包含两个角色：观察者和被观察对象。

被观察对象自身应该包含一个容器来存放观察者对象，当被观察者自身发生改变时通知容器内所有的观察者对象自动更新。

观察者对象可以注册到被观察者的中，完成注册后可以检测被观察者的变化，接收被观察者的通知。当然观察者也可以被注销掉，停止对被观察者的监控。

    复制代码
      1 /*
      2 * 关键代码：在目标类中增加一个ArrayList来存放观察者们。
      3 */
      4 #include <iostream>
      5 #include <list>
      6 #include <memory>
      7 ​
      8 using namespace std;
      9 ​
     10 class View;
     11 ​
     12 //被观察者抽象类   数据模型
     13 class DataModel
     14 {
     15 public:
     16     virtual ~DataModel(){}
     17     virtual void addView(View* view) = 0;
     18     virtual void removeView(View* view) = 0;
     19     virtual void notify() = 0;   //通知函数
     20 };
     21 ​
     22 //观察者抽象类   视图
     23 class View
     24 {
     25 public:
     26     virtual ~View(){ cout << "~View()" << endl; }
     27     virtual void update() = 0;
     28     virtual void setViewName(const string& name) = 0;
     29     virtual const string& name() = 0;
     30 };
     31 ​
     32 //具体的被观察类， 整数模型
     33 class IntDataModel:public DataModel
     34 {
     35 public:
     36     ~IntDataModel()
     37     {
     38         m_pViewList.clear();
     39     }
     40 ​
     41     virtual void addView(View* view) override
     42     {
     43         shared_ptr<View> temp(view);
     44         auto iter = find(m_pViewList.begin(), m_pViewList.end(), temp);
     45         if(iter == m_pViewList.end())
     46         {
     47             m_pViewList.push_front(temp);
     48         }
     49         else
     50         {
     51             cout << "View already exists" << endl;
     52         }
     53     }
     54 ​
     55     void removeView(View* view) override
     56     {
     57         auto iter = m_pViewList.begin();
     58         for(; iter != m_pViewList.end(); iter++)
     59         {
     60             if((*iter).get() == view)
     61             {
     62                 m_pViewList.erase(iter);
     63                 cout << "remove view" << endl;
     64                 return;
     65             }
     66         }
     67     }
     68 ​
     69     virtual void notify() override
     70     {
     71         auto iter = m_pViewList.begin();
     72         for(; iter != m_pViewList.end(); iter++)
     73         {
     74             (*iter).get()->update();
     75         }
     76     }
     77 ​
     78 private:
     79     list<shared_ptr<View>> m_pViewList; 
     80 };
     81 ​
     82 //具体的观察者类    表视图
     83 class TableView : public View
     84 {
     85 public:
     86     TableView() : m_name("unknow"){}
     87     TableView(const string& name) : m_name(name){}
     88     ~TableView(){ cout << "~TableView(): " << m_name.data() << endl; }
     89 ​
     90     void setViewName(const string& name)
     91     {
     92         m_name = name;
     93     }
     94 ​
     95     const string& name()
     96     {
     97         return m_name;
     98     }
     99 ​
    100     void update() override
    101     {
    102         cout << m_name.data() << " update" << endl;
    103     }
    104 ​
    105 private:
    106     string m_name;
    107 };
    108 ​
    109 int main()
    110 {
    111     /*
    112     * 这里需要补充说明的是在此示例代码中，View一旦被注册到DataModel类之后，DataModel解析时会自动解析掉     * 内部容器中存储的View对象，因此注册后的View对象不需要在手动去delete，再去delete View对象会出错。
    113     */
    114     
    115     View* v1 = new TableView("TableView1");
    116     View* v2 = new TableView("TableView2");
    117     View* v3 = new TableView("TableView3");
    118     View* v4 = new TableView("TableView4");
    119 ​
    120     IntDataModel* model = new IntDataModel;
    121     model->addView(v1);
    122     model->addView(v2);
    123     model->addView(v3);
    124     model->addView(v4);
    125 ​
    126     model->notify();
    127 ​
    128     cout << "-------------\n" << endl;
    129 ​
    130     model->removeView(v1);
    131 ​
    132     model->notify();
    133 ​
    134     delete model;
    135     model = nullptr;
    136 ​
    137     return 0;
    138 }
    139 ​

