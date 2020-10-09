## Key-Value Retrieval Networks for Task-Oriented Dialogue.

#### 数据描述



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