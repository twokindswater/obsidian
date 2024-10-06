---
cssclasses:
  - my_style_width_100
---

1. Behavior Data를 watch에서 다음과 같이 `start_time` , `end_time` 으로 전달 했는데
```
{
    "id":"device_id",
    "behaviors":[
        {
            "start_time": "1723126517088", # epoch time
			"end_time": "1723126517088",
            "action": "string/enum"
        },
        {
        },  ...
    ]
}
```

redis에서는 time_stamp 형식으로 나옴
```
10.2.0.20:6379> ZRANGEBYSCORE pet3/behavior/20240924 -inf +inf LIMIT 0 10
 1) "080946/eating"
 2) "080948/eating"
 3) "080948/walking"
 4) "080949/eating"
 5) "080949/walking"
 6) "080952/eating"
 7) "080952/walking"
 8) "081003/standing"
 9) "081003/walking"
10) "081004/standing"
```

2. Azure openAI는 variation 기능을 제공하지 않음.
variation : 전달 받은 파일을 변형
prompt 로 image 생성해야 됨. 
- pet breed, age, 성별 정보를 얻어 올 수 있어야 됨.
- AI diary 정보를 이용해서 prompt 작성. 