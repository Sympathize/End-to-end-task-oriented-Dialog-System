## DataSets

端到端的任务型对话的数据集格式与普通的数据集格式有一定差距，舍弃掉中间的slot，想用尽可能少的label信息得到好的response，提高模型的可部署性。

| Metric                  | DSTC2   | SMD     | MultiWOZ  |
| ----------------------- | ------- | ------- | --------- |
| # Dialogues             | 1,612   | 2,425   | 8,438     |
| Total # turns           | 23,354  | 12,732  | 115,424   |
| Total # tokens          | 199,431 | 121,977 | 1,520,970 |
| Avg. truns per dialogue | 14.49   | 5.25    | 13.68     |
| Avg. tokens per turn    | 8.54    | 8.02    | 13.18     |
| Total unique tokens     | 986     | 2,842   | 24,071    |
| # Slots                 | 8       | 13      | 25        |
| # Values                | 212     | 1363    | 4510      |

#### 数据实例

例如SMD数据，原始数据：

```
{
    "dialogue": [
      {
        "turn": "driver",
        "data": {
          "end_dialogue": false,
          "utterance": "remind me to take my pills"
        }
      },
      {
        "turn": "assistant",
        "data": {
          "end_dialogue": false,
          "requested": {
            "room": false,
            "agenda": false,
            "time": false,
            "date": false,
            "party": false,
            "event": true
          },
          "slots": {
            "event": "take pills"
          },
          "utterance": "What time do you need to take your pills?"
        }
      },
      {
        "turn": "driver",
        "data": {
          "end_dialogue": false,
          "utterance": "i need to take my pills at 7 pm."
        }
      },
      {
        "turn": "assistant",
        "data": {
          "end_dialogue": true,
          "requested": {
            "room": false,
            "agenda": false,
            "time": true,
            "date": false,
            "party": false,
            "event": true
          },
          "slots": {
          	"time": "7pm"
          },
          "utterance": "Ok setting your medicine appointment for 7pm"
        }
      }
    ],
    "scenario": {
      "kb": {
        "items": null,
        "column_names": [
          "event",
          "time",
          "date",
          "room",
          "agenda",
          "party"
        ],
        "kb_title": "calendar"
      },
      "task": {
        "intent": "schedule"
      },
      "uuid": "e6a4e9dc-a952-47dc-bb7f-3586cdb1c3ff"
    }
  },
```

处理过后的数据：

```
#schedule#
1 remind me to take my pills	what time do you need to take your pills ?	[]
2 i need to take my pills at 7pm	ok setting your medicine appointment for 7pm	['7pm']
```

