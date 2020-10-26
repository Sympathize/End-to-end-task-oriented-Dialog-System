# MultiWOZ

跨**多个领域**和主题的**完全标记**的数据集，主要就是大，数据集包括以下几个领域的任务型对话：

 1: restaurant, 2: hotel, 3: attraction, 4: taxi, 5: train, 6: hospital, 7: police.

#### 数据分析

本数据集一共收集了10,438组对话，有70%超过了10轮，单域和多域对话的平均轮数分别为8.93轮和15.39轮。

向导的对话轮数最多平均轮数11.75和15.12，response也更加复杂，所以可以训练更复杂的模型。

#### 数据实例

```
#hotel#
0|[archway_house]|['[address 52_gilbert_road]', '[area north]', '[internet yes]', '[parking yes]', '[phone 01223575314]', '[postcode cb43pe]', '[singleprice 40]', '[doubleprice 70]', '[pricerange moderate]', '[stars 4]', '[takesbookings yes]', '[type guesthouse]']
0|[address 52_gilbert_road]|['[archway_house]']
0|[area north]|['[archway_house]', '[ashley_hotel]', '[worth_house]', '[hamilton_lodge]']
0|[internet yes]|['[archway_house]', '[gonville_hotel]', '[leverton_house]', '[ashley_hotel]', '[worth_house]', '[hamilton_lodge]']
0|[parking yes]|['[archway_house]', '[gonville_hotel]', '[leverton_house]', '[ashley_hotel]', '[worth_house]', '[hamilton_lodge]']
0|[phone 01223575314]|['[archway_house]']
0|[postcode cb43pe]|['[archway_house]']
0|[singleprice 40]|['[archway_house]', '[leverton_house]']
0|[doubleprice 70]|['[archway_house]']
0|[pricerange moderate]|['[archway_house]', '[ashley_hotel]', '[hamilton_lodge]']
0|[stars 4]|['[archway_house]', '[leverton_house]', '[worth_house]']
0|[takesbookings yes]|['[archway_house]', '[gonville_hotel]', '[leverton_house]', '[ashley_hotel]', '[worth_house]', '[hamilton_lodge]']
0|[type guesthouse]|['[archway_house]', '[leverton_house]', '[worth_house]', '[hamilton_lodge]']
0|[gonville_hotel]|['[address gonville_place]', '[area centre]', '[internet yes]', '[parking yes]', '[phone 01223366611]', '[postcode cb11ly]', '[singleprice 79]', '[doubleprice 95]', '[familyprice 119]', '[pricerange expensive]', '[stars 3]', '[takesbookings yes]', '[type hotel]']
0|[address gonville_place]|['[gonville_hotel]']
0|[area centre]|['[gonville_hotel]']
0|[phone 01223366611]|['[gonville_hotel]']
0|[postcode cb11ly]|['[gonville_hotel]']
0|[singleprice 79]|['[gonville_hotel]']
0|[doubleprice 95]|['[gonville_hotel]']
0|[familyprice 119]|['[gonville_hotel]']
0|[pricerange expensive]|['[gonville_hotel]']
0|[stars 3]|['[gonville_hotel]', '[hamilton_lodge]']
0|[type hotel]|['[gonville_hotel]', '[ashley_hotel]']
0|[leverton_house]|['[address 732-734_newmarket_road]', '[area east]', '[internet yes]', '[parking yes]', '[phone 01223292094]', '[postcode cb58rs]', '[singleprice 40]', '[doubleprice 60]', '[familyprice 90]', '[pricerange cheap]', '[stars 4]', '[takesbookings yes]', '[type guesthouse]']
0|[address 732-734_newmarket_road]|['[leverton_house]']
0|[area east]|['[leverton_house]']
0|[phone 01223292094]|['[leverton_house]']
0|[postcode cb58rs]|['[leverton_house]']
0|[doubleprice 60]|['[leverton_house]', '[worth_house]']
0|[familyprice 90]|['[leverton_house]']
0|[pricerange cheap]|['[leverton_house]', '[worth_house]']
0|[ashley_hotel]|['[address 74_chesterton_road]', '[area north]', '[internet yes]', '[parking yes]', '[phone 01223350059]', '[postcode cb41er]', '[doubleprice 75]', '[familyprice 85]', '[pricerange moderate]', '[stars 2]', '[takesbookings yes]', '[type hotel]']
0|[address 74_chesterton_road]|['[ashley_hotel]']
0|[phone 01223350059]|['[ashley_hotel]']
0|[postcode cb41er]|['[ashley_hotel]']
0|[doubleprice 75]|['[ashley_hotel]']
0|[familyprice 85]|['[ashley_hotel]', '[worth_house]', '[hamilton_lodge]']
0|[stars 2]|['[ashley_hotel]']
0|[worth_house]|['[address 152_chesterton_road]', '[area north]', '[internet yes]', '[parking yes]', '[phone 01223316074]', '[postcode cb41da]', '[singleprice 49]', '[doubleprice 60]', '[familyprice 85]', '[pricerange cheap]', '[stars 4]', '[takesbookings yes]', '[type guesthouse]']
0|[address 152_chesterton_road]|['[worth_house]']
0|[phone 01223316074]|['[worth_house]']
0|[postcode cb41da]|['[worth_house]', '[hamilton_lodge]']
0|[singleprice 49]|['[worth_house]']
0|[hamilton_lodge]|['[address 156_chesterton_road]', '[area north]', '[internet yes]', '[parking yes]', '[phone 01223365664]', '[postcode cb41da]', '[singleprice 50]', '[doubleprice 73]', '[familyprice 85]', '[pricerange moderate]', '[stars 3]', '[takesbookings yes]', '[type guesthouse]']
0|[address 156_chesterton_road]|['[hamilton_lodge]']
0|[phone 01223365664]|['[hamilton_lodge]']
0|[singleprice 50]|['[hamilton_lodge]']
0|[doubleprice 73]|['[hamilton_lodge]']
1 i need a place to stay in the north please	there are 13 places to stay in the north do you have any other criteria ?	['north']
2 i don t want to have to pay for parking	i have 5 different gueshouses listed for what day and for how many please ?	[]
3 for 3 people starting on wednesday and staying 2 nights	there are 11 hotels available actually would you like to narrow it to a specific price range or star rating ?	[]
4 just a guesthouse in the north with free parking i ll need a reference number then too please	i was able to get you in at archway_house your reference number is wumuz0jx can i help you with anything else ?	['archway_house']
5 that s all i need today thanks ! bye !	thank you for using our system !	[]
```

