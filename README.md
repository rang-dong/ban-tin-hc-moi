# NOTE
Chưa có bản tin cài đặt cảnh cho các thiết bị :Màn hình, remote, cảm biến cửa, socket, switch, IR 

# ĐIỀU KHIỂN
## ĐIỀU KHIỂN DEVICE
1. Json mẫu
```json
{
   "CMD": "DEVICE",
   "DATA": 
    {
          "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653", 
          "PROPERTIES":[
                 { 
                        "ID": 0,
                        "VALUE": 1
                } 
         ]       
    }    
} 
```
2. Giải thích
Điều khiển một thiết bị có ID “b717f8d8-6f18-43c0-ae46-69c32998f653”, thiết lập giá trị cho thuộc tính có ID=0 thành 1
3. Bản tin phản hồi
Giống bản tin gửi đi nhưng được gửi vào topic phản hồi

## ĐIỀU KHIỂN GROUP
1. Json mẫu
```json
{
   "CMD": "GROUP",
   "DATA": 
    {
          "GROUP_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653", 
          "PROPERTIES":[
                { 
                    "ID": 0,
                    "VALUE": 1
                } 
         ]       
    }    
}
```
2. Giải thích
Điều khiển nhóm có ID=b717f8d8-6f18-43c0-ae46-69c32998f653, thiết lập giá trị thuộc tính ID=0 thành 1 cho tất cả các thiết bị trong nhóm
3. Json phản hồi:
Là bản tin phản hồi của điều khiển device

## ĐIỀU KHIỂN SCENE
1. Json mẫu
```json
{
   "CMD": "EVENT_TRIGGER",
   "DATA": 
    {
        "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2"
    }    
}
```
2. Giải thích
Kích hoạt SCENE có ID=aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2
3. Bản tin phản hồi
```json
{
   "CMD": "EVENT_TRIGGER",
   "DATA": 
    {
       "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
       "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653"
    }    
}
```

# CẤU HÌNH
## GROUP
### Tạo group
1. Json mẫu
```json
{
      "CMD": "GROUP",
      "TYPE": "CREATE",
      "DATA": {
           "GROUP_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
           "CATEGORY_ID": 12,
           "NAME": "abc",
           "DEVICES": [
                "b717f8d8-6f18-43c0-ae46-69c32998f653",
                "b717f8d8-6f18-43c0-ae46-69c32998f654"
            ]
      }
}
```
2. Giải thích:
Tạo một nhóm mới gồm 2 thiết bị
Nếu không có thiết bị thì trường sẽ để trống: "DEVICE":[]
3. Json phản hồi
```json
{
      "CMD": "GROUP",
      "TYPE": "CREATE",
      "DATA": {
           "GROUP_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
           "CATEGORY_ID": 12,
           "NAME": "abc"
           "STATUS": "SUCCESS"
      }
}

{
      "CMD": "GROUP",
      "TYPE": "ADD_DEVICE",
      "DATA": {
           "GROUP_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
           "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
           "STATUS": "SUCCESS"
      }
}

```
### Xóa device khỏi nhóm
1. Json mẫu
```json
{
      "CMD": "GROUP",
      "TYPE": "REMOVE_DEVICE",
      "DATA": {
           "GROUP_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
            "DEVICES": [
                "b717f8d8-6f18-43c0-ae46-69c32998f653",
                "b717f8d8-6f18-43c0-ae46-69c32998f654"
            ]
      }
}
```
2. Giải thích
Xóa 2 thiết bị khỏi nhóm
3. Json phản hồi
```json
{
      "CMD": "GROUP",
      "TYPE": "REMOVE_DEVICE",
      "DATA": {
           "GROUP_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
           "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
          "STATUS": "SUCCESS"
      }
}
```
### Thêm device vào group
1. Json mẫu
```json
{
      "CMD": "GROUP",
      "TYPE": "ADD_DEVICE",
      "DATA": {
           "GROUP_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
            "DEVICES": [
                "b717f8d8-6f18-43c0-ae46-69c32998f653",
                "b717f8d8-6f18-43c0-ae46-69c32998f654"
            ]
      }
}
```
2. Giải thích
Thêm 2 device vào group
3. Json phản hồi
```json
{
     "CMD": "GROUP",
     "TYPE": "ADD_DEVICE",
     "DATA": {
          "GROUP_ID": "aa3549d4-5471-4d75-b0b2-b70fa5c10fb2",
          "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
          "STATUS": "SUCCESS"
      }
}
```

### Xóa toàn bộ device của group
1. Json mẫu
```json
{
      "CMD": "GROUP",
      "TYPE": "DELETE",
      "DATA":
      {
             "GROUP_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2"
      }      
}
```
2. Giải thích
Xóa toàn bộ device ra khỏi group
3. Json phản hồi
```json
{
     "CMD": "GROUP",
     "TYPE": "DEVICE_RESPONSE",
     "DATA": {
          "GROUP_ID": "aa3549d4-5471-4d75-b0b2-b70fa5c10fb2",
          "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
          "STATUS": "SUCCESS"
      }
}
```
## DEVICE
### Thêm device vào mạng
1. Json mẫu
```json
{
     "CMD":"SCAN"
}
```
2. Giải thích
Thêm device vào mạng
3. Json phản hồi
```json
{
   "CMD": "TYPE_DEVICE",
   "DATA": 
           {
                   "DEVICE_ID": "b717f8d86f1843c0ae4669c32998f653", 
                   "DEVICE_KEY": "b717f8d86f1843c0ae4669c32998f653",
                   "NET_KEY": "b717f8d86f1843c0ae4669c32998f653",
                   "APP_KEY": "b717f8d86f1843c0ae4669c32998f653",
                   "CATEGORY_ID":   23002                
           }   
}
```
### Dừng quá trình đưa thiết bị vào mạng
1. Json mẫu
```json
{
     "CMD":"STOP"
}
```
2. Giải thích
Dừng quá trình đưa thiết bị vào mạng
3. Json phản hồi
```json
{
     "CMD":"STOP"
}
```
### Xóa device trong mạng
1. Json mẫu
```json
{
   "CMD":"RESET_NODE",
   "DATA":[
      "b717f8d8-6f18-43c0-ae46-69c32998f653",
      "b717f8d8-6f18-43c0-ae46-69c32998f654"
   ]
}
```
2. Giải thích
Xóa device trong mạng
3. Json phản hồi
```json
{
     "CMD":"RESET_NODE",
     "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653"
}
```
## SCENE
### Tạo scene
1. Json mẫu
```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "CREATE",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "GROUP_ID": "97ab44a3-e788-46a1-9c07-79f39d6be33f",
    "EVENT_TRIGGER_TYPE_ID": 1,
    "PRIORITY": 1,
    "HAS_TIMER": 1,
    "START_AT": "10:56:1",
    "END_AT": "11:1:15",
    "EACH_DAY":["EACHMONDAY","EACHTUESDAY"],
    "DEVICES": [
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
        "DEVICE_TYPE_ID":12001,
        "PROPERTIES": [
          {
            "ID": 0,
            "VALUE": 1
          }
        ]
      },
      {
        "DEVICE_ID": "bb3549d4-5471-4d75-b0b2- b70fa5c10fb2",
        "DEVICE_TYPE_ID":14001,
        "PROPERTIES": [
          {
            "ID": 0,
            "VALUE": 1
          }
        ]
      },
      {
        "DEVICE_ID": "cc3549d4-5471-4d75-b0b2- b70fa5c10fb2",
        "DEVICE_TYPE_ID":14001,
        "PROPERTIES": [
          {
            "ID": 7,
            "VALUE": 1
          }
        ]
      }
    ]
  }
}
```
2. Giải thích
Tạo scene với device và group tương ứng
3. Json phản hồi
```json
{
      "CMD": "EVENT_TRIGGER",
      "TYPE": "CREATE",
      "DATA": {
           "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
           "GROUP_ID": "97ab44a3-e788-46a1-9c07-79f39d6be33f",
           "EVENT_TRIGGER_TYPE_ID": 1
        }
}
```
### Edit scene
1. Json mẫu
```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "EDIT",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "GROUP_ID": "97ab44a3-e788-46a1-9c07-79f39d6be33f",
    "EVENT_TRIGGER_TYPE_ID": 1,
    "PRIORITY": 1,
    "HAS_TIMER": 1,
    "START_AT": "10:56:1",
    "END_AT": "11:1:15",
    "EACH_DAY":["EACHMONDAY","EACHTUESDAY"],
    "DEVICES": [
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
        "DEVICE_TYPE_ID":14001,
        "TYPE":"EDIT",
        "PROPERTIES": [
           {
            "ID": 23,
            "VALUE": 6
          }
        ]
      },
       {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10f00",
        "DEVICE_TYPE_ID":14001,
        "TYPE":"DEL",
        "PROPERTIES": [
           {
            "ID": 23,
            "VALUE": 6
          }
        ]
      }
    ]
  }
}
```
2. Giải thích
Bản tin giống với bản tin tạo scene nhưng có thêm trường type "EDIT" HC sẽ thực hiện sửa scene cho device; "DEL" HC sẽ xóa device ra khỏi scene
3. Json phản hồi
```json
{
      "CMD": "EVENT_TRIGGER",
      "TYPE": "EDIT",
      "DATA": {
           "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
           "GROUP_ID": "97ab44a3-e788-46a1-9c07-79f39d6be33f",
           "EVENT_TRIGGER_TYPE_ID": 1
        }
}
```
### Xóa Scene
1. Json mẫu
```json
{
      "CMD": "EVENT_TRIGGER",
      "TYPE": "DELETE",
      "DATA": {
           "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2"
        }
}
```
2. Giải thích
Xóa scene với ID tương ứng
3. Json phản hồi
```json
{
      "CMD": "EVENT_TRIGGER",
      "TYPE": "DELETE",
      "DATA": {
           "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2"
        }
}
```
## RULE
### Tạo rule
1. Json mẫu
```json
{
   "CMD":"EVENT_TRIGGER",
   "TYPE":"CREATE",
   "DATA":{
      "EVENT_TRIGGER_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
      "GROUP_ID":"97ab44a3-e788-46a1-9c07-79f39d6be33f",
      "EVENT_TRIGGER_TYPE_ID":2,
      "PRIORITY":3,
      "HAS_TIMER":1,
      "START_AT":"10:56",
      "END_AT":"11:1",
      "HAS_REPEATER":1,
      "EACH_DAY":[
         "EACHMONDAY",
         "EACHTUESDAY"
      ],
      "LOGICAL_OPERATOR_ID":0,
      "STATUS_ID":1,
      "INPUT_DEVICE":[
         {
            "DEVICE_ID":"aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
            "DATA":{
               "COMPARISON_OPERATOR_ID":1,
               "DEVICE_ATTRIBUTE_ID":12,
               "EVENT_TRIGGER_TYPE_ID":1,
               "DEVICE_ATTRIBUTE_VALUE":
           {
             "BUTTON_VALUE": "BUTTON_1",
             "MODE_VALUE": 1
           } 
            }
         }
      ],
      "OUTPUT_DEVICE":{
         "DEVICES":[
            {
               "TYPE_RUN":0,
               "DEVICE_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
               "PROPERTIES":[
                  {
                     "ID":0,
                     "VALUE":1
                  },
                  {
                     "ID":2,
                     "VALUE":50
                  }
               ]
            },
            { 
               "TYPE_RUN":0,
               "DEVICE_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb26666666666666",
               "PROPERTIES":[
                  {
                     "ID":0,
                     "VALUE":1
                  }
               ]
            }
         ],
         "GROUPS":[
            {
               "TYPE_RUN":1,
               "GROUP_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
               "PROPERTIES":[
                  {
                     "ID":0,
                     "VALUE":0
                  }
               ]
            }
         ],
         "SCENE":[
            {
               "TYPE_RUN":0,
               "SCENE_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2"
            }
         ]
      }
   }
}
```
2. Giải thích
Tạo rule với giá trị được set up với mỗi device, scene, group sẽ có 1 trường để phân biệt nó được kích hoạt ở thời gian nào "TYPE_RUN"=0 "START_AT", "TYPE_RUN"=1 "END_AT"
3. Json phản hồi
```json
{
  "CMD": "EVENT_TRIGGER",
  "DATA":{
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "STATUS": "SUCCESS"
  }
}
```
### Edit rule
1. Json mẫu
```json
{
   "CMD":"EVENT_TRIGGER",
   "TYPE":"EDIT",
   "DATA":{
      "EVENT_TRIGGER_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
      "GROUP_ID":"97ab44a3-e788-46a1-9c07-79f39d6be33f",
      "EVENT_TRIGGER_TYPE_ID":2,
      "PRIORITY":3,
      "HAS_TIMER":1,
      "START_AT":"10:56:1",
      "END_AT":"11:1:15",
      "HAS_REPEATER":1,
      "EACH_DAY":[
         "EACHMONDAY",
         "EACHTUESDAY"
      ],
      "LOGICAL_OPERATOR_ID":-1,
      "STATUS_ID":1,
      "INPUT_DEVICE":[
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
        "TYPE":"DEL",
        "DATA":{}
      },
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
        "TYPE":"EDIT",
        "DATA":{
          "LIGHT_SENSOR": 
           {
              "LOW_LUX":200,
              "HIGHT_LUX":600,
              "COMPARISON_OPERATOR_ID":7,
              "DEVICE_ATTRIBUTE_ID": 12
            },
           "PIR_SENSOR": 
           {
              "PIR":1,
              "COMPARISON_OPERATOR_ID":1,
              "DEVICE_ATTRIBUTE_ID": 12
            }
        }
      },
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
        "TYPE":"ADD",
        "DATA":{
          "LIGHT_SENSOR": 
           {
              "LOW_LUX":200,
              "HIGHT_LUX":600,
              "COMPARISON_OPERATOR_ID":7,
              "DEVICE_ATTRIBUTE_ID": 12
            },
           "PIR_SENSOR": 
           {
              "PIR":1,
              "COMPARISON_OPERATOR_ID":1,
              "DEVICE_ATTRIBUTE_ID": 12
            }
        }
      }
     ],
        "OUTPUT_DEVICE":{
          "DEVICES":[
         {
            "TYPE_RUN":1,
            "DEVICE_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
            "TYPE":"DEL",
            "PROPERTIES":[]
         },
         {
            "TYPE_RUN":1,
            "DEVICE_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
            "TYPE":"EDIT",
            "PROPERTIES":[
               {
                  "ID":0,
                  "VALUE":1
               },
               {
                  "ID":2,
                  "VALUE":50
               }
            ]
         },
         {
            "TYPE_RUN":1,
            "DEVICE_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
            "TYPE":"ADD",
            "PROPERTIES":[
               {
                  "ID":0,
                  "VALUE":1
               },
               {
                  "ID":2,
                  "VALUE":50
               }
            ]
         }
      ],
      "GROUPS":[
         {
            "TYPE_RUN":1,
            "GROUP_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
            "TYPE":"DEL",
            "PROPERTIES":[]
         },
         {
            "TYPE_RUN":1,
            "GROUP_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
            "TYPE":"EDIT",
            "PROPERTIES":[
               {
                  "ID":0,
                  "VALUE":1
               },
               {
                  "ID":2,
                  "VALUE":50
               }
            ]
         },
         {
            "TYPE_RUN":1,
            "GROUP_ID":"aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
            "TYPE":"ADD",
            "PROPERTIES":[
               {
                  "ID":0,
                  "VALUE":1
               },
               {
                  "ID":2,
                  "VALUE":50
               }
            ]
         }
      ],
      "SCENE":[
       {
          "TYPE_RUN":1,
          "SCENE_ID":"abbbcccccc",
          "TYPE":"DEL"
       },
       {
          "TYPE_RUN":1,
          "SCENE_ID":"abbbcccccc",
          "TYPE":"ADD"
       }
      ]
          
        }
      
   }
}
```
2. Giải thích
Giống bản tin tạo rule nhưng type là "EDIT"
3. Json phản hồi
```json
{
  "CMD": "EVENT_TRIGGER",
  "DATA":{
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "STATUS": "SUCCESS"
  }
}
```
### Xóa rule
1. Json mẫu
```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "DELETE",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2"
  }
}
```
2. Giải thích
Xóa rule
3. Json phản hồi
```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "DELETE",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2"
  }
}
```
### Thay đổi trạng thái kích hoạt
1. Json mẫu
```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "STATUS",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "STATUS_ID": 0
  }
}
```
2. Giải thích
Thay đổi trạng thái kích hoạt của rule
3. Json phản hồi
```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "STATUS",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "STATUS_ID": 0
  }
}
```
# MỘT SỐ BẢN TIN ĐẠC BIỆT
1. Bản tin phản hồi thiệt độ, độ ẩm, bụi mịn :2.5;10;1.0
```json
{
  "CMD":"SENSOR_VALUE",
  "DATA":{
    "DEVICE_ID":"b717f8d8-6f18-43c0-ae46-69c32998f653",
    "TEMPERATURE_VALUE":30
  }
}
{
  "CMD":"SENSOR_VALUE",
  "DATA":{
    "DEVICE_ID":"b717f8d8-6f18-43c0-ae46-69c32998f653",
    "HUMIDITY_VALUE":30
  }
}
{
  "CMD":"SENSOR_VALUE",
  "DATA":{
    "DEVICE_ID":"b717f8d8-6f18-43c0-ae46-69c32998f653",
    "PM2.5_VALUE":30
  }
}
{
  "CMD":"SENSOR_VALUE",
  "DATA":{
    "DEVICE_ID":"b717f8d8-6f18-43c0-ae46-69c32998f653",
    "PM1_VALUE":30
  }
}
{
  "CMD":"SENSOR_VALUE",
  "DATA":{
    "DEVICE_ID":"b717f8d8-6f18-43c0-ae46-69c32998f653",
    "PM10_VALUE":30
  }
}
```
2. Bản tin phản hồi trạng thái cảm biến khói
```json
{
  "CMD": "SENSOR_VALUE",
  "DATA": {
    "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "SMOKE_VALUE":1
  }
}
```
3. Bản tin phản hồi trạng thái nút nhấn
```json
{
  "CMD": "REMOTE",
  "DATA": {
    "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "BUTTON_VALUE": "BUTTON_1",
    "MODE_VALUE": 1
  }
}
```
4. Bản tin HC kết nối Cloud
```json
{
  "CMD":"HC_CONNECT_TO_CLOUD",
  "DATA":{
    "END_USER_PROFILE_ID":10039,
    "REFRESH_TOKEN":"ABCGKGHLKHFSKLHDF"
  }
}
```
