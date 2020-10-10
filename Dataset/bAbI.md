## Learning End-to-End Goal-Oriented Dialog.

### 数据描述

为了验证end2end的任务型对话系统的效果，论文构建了7个在线订餐的数据集，包括：

- 5个模拟的数据集
- 1个DSTC2（Dialog State Tracking Challenge）改造过来的真实数据集
- 1个真实用户和真人操作员之间的真实数据集

作者在这些数据集上进行了多种模型的实验，包括基于规则的系统、基于经典信息抽取的方法、有监督embeddings方法、end2end的记忆网络MemN2N，并得出记忆网络效果最好的结论。

每个任务包括训练集+验证集+测试集三个语料，每个语料有1000个对话。对话之间用空行隔开，同一个对话用id标识每一轮，每一轮一行，包括用户说话和bot说话，用 $\t$ 隔开。句子中以`<SILENCE>`开头的是需要预测的句子。此外。每个任务还包括一个有**OOV**词的测试集，即存在不在训练集出现过的实体名，但是在kb(知识库)出现过。

5个任务共用一个kb，即文件dialog-babi-kb-all.txt，里面记录了每个餐厅的位置、电话、档次等信息；此外还共用一个候选句子库，即文件dialog-babi-candidates.txt，该文件包括5个task里面所有训练集+验证集+2个测试集里面bot说的话。**因此任务是从候选句子中选出`<SILENCE>`最可能的句子，而不是逐词生成`<SILENCE>`代表的句子。**

### 数据格式/任务介绍

#### Task1

bot（机器人）能通过调用api来查询kb(知识库)，从而获得餐厅的类型、距离、电话、地址等信息，调用api需要4个字段，分别为（餐厅类型、地点、就餐人数、档次）。该任务用于评估当用户提供的信息少于4个字段时，**bot是否能通过询问补充剩余的字段**，从而发起api调用kb。

###### 实例

```
1 hello	hello what can i help you with today
2 can you book a table for six people with french food	i'm on it
3 <SILENCE>	where should it be
4 in bombay	which price range are looking for
5 i am looking for a cheap restaurant	ok let me look into some options for you
6 <SILENCE>	api_call french bombay six cheap
```

#### Task2

测试修改API调用的能力

###### 实例

```
1 good morning	hello what can i help you with today
2 can you book a table in a moderate price range with british cuisine for eight people in rome	i'm on it
3 <SILENCE>	ok let me look into some options for you
4 <SILENCE>	api_call british rome eight moderate
5 instead could it be for six people	sure is there anything else to update
6 instead could it be in bombay	sure is there anything else to update
7 instead could it be with italian food	sure is there anything else to update
8 actually i would prefer in a expensive price range	sure is there anything else to update
9 no	ok let me look into some options for you
10 <SILENCE>	api_call italian bombay six expensive
11 thanks	you're welcome
```

#### Task3

当bot通过api调用得到相关度最高的几个餐厅时，验证bot是否有能力向用户建议其中的一些餐厅。数据集只包括至少有3个候选餐厅的对话。

###### 实例

```
1 resto_madrid_cheap_british_2stars R_phone resto_madrid_cheap_british_2stars_phone
2 resto_madrid_cheap_british_2stars R_cuisine british
3 resto_madrid_cheap_british_2stars R_address resto_madrid_cheap_british_2stars_address
4 resto_madrid_cheap_british_2stars R_location madrid
5 resto_madrid_cheap_british_2stars R_number four
6 resto_madrid_cheap_british_2stars R_price cheap
7 resto_madrid_cheap_british_2stars R_rating 2
8 resto_madrid_cheap_british_6stars R_phone resto_madrid_cheap_british_6stars_phone
9 resto_madrid_cheap_british_6stars R_cuisine british
10 resto_madrid_cheap_british_6stars R_address resto_madrid_cheap_british_6stars_address
11 resto_madrid_cheap_british_6stars R_location madrid
12 resto_madrid_cheap_british_6stars R_number four
13 resto_madrid_cheap_british_6stars R_price cheap
14 resto_madrid_cheap_british_6stars R_rating 6
15 resto_madrid_cheap_british_7stars R_phone resto_madrid_cheap_british_7stars_phone
16 resto_madrid_cheap_british_7stars R_cuisine british
17 resto_madrid_cheap_british_7stars R_address resto_madrid_cheap_british_7stars_address
18 resto_madrid_cheap_british_7stars R_location madrid
19 resto_madrid_cheap_british_7stars R_number four
20 resto_madrid_cheap_british_7stars R_price cheap
21 resto_madrid_cheap_british_7stars R_rating 7
22 resto_madrid_cheap_british_8stars R_phone resto_madrid_cheap_british_8stars_phone
23 resto_madrid_cheap_british_8stars R_cuisine british
24 resto_madrid_cheap_british_8stars R_address resto_madrid_cheap_british_8stars_address
25 resto_madrid_cheap_british_8stars R_location madrid
26 resto_madrid_cheap_british_8stars R_number four
27 resto_madrid_cheap_british_8stars R_price cheap
28 resto_madrid_cheap_british_8stars R_rating 8
29 good morning	hello what can i help you with today
30 can you book a table	i'm on it
31 <SILENCE>	any preference on a type of cuisine
32 with british cuisine	where should it be
33 madrid please	how many people would be in your party
34 we will be four	which price range are looking for
35 i am looking for a cheap restaurant	ok let me look into some options for you
36 <SILENCE>	what do you think of this option: resto_madrid_cheap_british_8stars
37 do you have something else	sure let me find an other option for you
38 <SILENCE>	what do you think of this option: resto_madrid_cheap_british_7stars
39 that looks great	great let me do the reservation
```

#### Task4

当用户接受了bot提议的某个餐厅，并询问该餐厅更加详细的信息时，验证bot是否有能力提供额外的信息，如餐厅地址等。

###### 实例

```
1 resto_paris_cheap_spanish_7stars R_phone resto_paris_cheap_spanish_7stars_phone
2 resto_paris_cheap_spanish_7stars R_cuisine spanish
3 resto_paris_cheap_spanish_7stars R_address resto_paris_cheap_spanish_7stars_address
4 resto_paris_cheap_spanish_7stars R_location paris
5 resto_paris_cheap_spanish_7stars R_number two
6 resto_paris_cheap_spanish_7stars R_price cheap
7 resto_paris_cheap_spanish_7stars R_rating 7
8 hello	hello what can i help you with today
9 may i have a table at resto_paris_cheap_spanish_7stars	great let me do the reservation
10 do you have its address	here it is resto_paris_cheap_spanish_7stars_address
```

#### Task5

验证bot是否包括上述4种能力。有task3不同的是，这里包括查询kb后候选餐厅少于3家的情况。

###### 实例

```
1 good morning	hello what can i help you with today
2 can you make a restaurant reservation in rome in a cheap price range	i'm on it
3 <SILENCE>	any preference on a type of cuisine
4 with spanish food	how many people would be in your party
5 we will be six	ok let me look into some options for you
6 <SILENCE>	api_call spanish rome six cheap
7 instead could it be in a expensive price range	sure is there anything else to update
8 no	ok let me look into some options for you
9 <SILENCE>	api_call spanish rome six expensive
10 resto_rome_expensive_spanish_6stars R_phone resto_rome_expensive_spanish_6stars_phone
11 resto_rome_expensive_spanish_6stars R_cuisine spanish
12 resto_rome_expensive_spanish_6stars R_address resto_rome_expensive_spanish_6stars_address
13 resto_rome_expensive_spanish_6stars R_location rome
14 resto_rome_expensive_spanish_6stars R_number six
15 resto_rome_expensive_spanish_6stars R_price expensive
16 resto_rome_expensive_spanish_6stars R_rating 6
17 resto_rome_expensive_spanish_7stars R_phone resto_rome_expensive_spanish_7stars_phone
18 resto_rome_expensive_spanish_7stars R_cuisine spanish
19 resto_rome_expensive_spanish_7stars R_address resto_rome_expensive_spanish_7stars_address
20 resto_rome_expensive_spanish_7stars R_location rome
21 resto_rome_expensive_spanish_7stars R_number six
22 resto_rome_expensive_spanish_7stars R_price expensive
23 resto_rome_expensive_spanish_7stars R_rating 7
24 resto_rome_expensive_spanish_2stars R_phone resto_rome_expensive_spanish_2stars_phone
25 resto_rome_expensive_spanish_2stars R_cuisine spanish
26 resto_rome_expensive_spanish_2stars R_address resto_rome_expensive_spanish_2stars_address
27 resto_rome_expensive_spanish_2stars R_location rome
28 resto_rome_expensive_spanish_2stars R_number six
29 resto_rome_expensive_spanish_2stars R_price expensive
30 resto_rome_expensive_spanish_2stars R_rating 2
31 <SILENCE>	what do you think of this option: resto_rome_expensive_spanish_7stars
32 do you have something else	sure let me find an other option for you
33 <SILENCE>	what do you think of this option: resto_rome_expensive_spanish_6stars
34 no this does not work for me	sure let me find an other option for you
35 <SILENCE>	what do you think of this option: resto_rome_expensive_spanish_2stars
36 let's do it	great let me do the reservation
37 do you have its phone number	here it is resto_rome_expensive_spanish_2stars_phone
38 do you have its address	here it is resto_rome_expensive_spanish_2stars_address
39 you rock	is there anything i can help you with
40 no thank you	you're welcome
```

