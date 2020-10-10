## Key-Value Retrieval Networks for Task-Oriented Dialogue.

#### 数据描述

该数据集是有关于车载对话数据集，多回合对话的数据是用Wizard-of-Oz方案来收集的(Wizard-of-Oz意思为由人替代机器，以完成数据收集)

对话有三个领域`navigate`，`schedule`，`weather`

#### 数据格式

```
[
	#一个字典表示一组数据，数据中包括两部分，对话和情景数据库
	{
		#每轮data中有turn和data，用户的data中有是否是结束语和说话内容，响应多了requested和slots模块
		"dialogue":[
			{
				"turn":"driver",
				"data":{
					"end_dialogue": 
					"utterance": 
				}
			},
			{
				"turn":"assistant"
				"data":{
					"end_dialogue": 
					"requested":{
						"distance": 
						"traffic_info":
						"poi_type":
						"address":
						"poi":
					},
					"slots":{
						"distance":
						"poi_type":
					}
					"utterance":
				}
			},
			......
		]
		
		"scenario"{
			"kb":{
				"items":[
				
				],
				"column_names":[
				
				],
				"kb_title":
			},
			"task":{
				"intent":
			},
			"uuid":
		}
	}
]
```