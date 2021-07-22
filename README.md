# NOTE
Chưa có bản tin cài đặt cảnh cho các thiết bị :Màn hình, socket, switch, IR 

# ĐIỀU KHIỂN

## ĐIỀU KHIỂN DEVICE

1. Json mẫu

```json
{
  "CMD": "DEVICE",
  "DATA": {
    "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "PROPERTIES": [
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
  "DATA": {
    "GROUP_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "PROPERTIES": [
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

3. Json phản hồi

Là bản tin phản hồi của điều khiển device:

```json
{
  "CMD": "DEVICE",
  "DATA": {
    "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "PROPERTIES": [
      {
        "ID": 0,
        "VALUE": 1
      }
    ]
  }
} 
```

## ĐIỀU KHIỂN SCENE

1. Json mẫu

```json
{
  "CMD": "EVENT_TRIGGER",
  "DATA": {
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
  "DATA": {
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

Tạo một nhóm mới gồm 2 thiết bị.
Nếu không có thiết bị thì trường sẽ để trống: "DEVICE":[]

3. Json phản hồi

```json
{
  "CMD": "GROUP",
  "TYPE": "CREATE",
  "DATA": {
    "GROUP_ID": "aa3549d4-5471-4d75-b0b2-b70fa5c10fb2",
    "DEVICE_ID": [
      "b717f8d8-6f18-43c0-ae46-69c32998f653",
      "b717f8d8-6f18-43c0-ae46-69c32998f654"
    ],
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
    "DEVICE_ID": [
      "b717f8d8-6f18-43c0-ae46-69c32998f653",
      "b717f8d8-6f18-43c0-ae46-69c32998f654"
    ],
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
  "TYPE": "CREATE",
  "DATA": {
    "GROUP_ID": "aa3549d4-5471-4d75-b0b2-b70fa5c10fb2",
    "GROUP_UNICAST_ID": 49152,
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
  "DATA": {
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
  "TYPE": "DELETE",
  "DATA": {
    "GROUP_ID": "aa3549d4-5471-4d75-b0b2-b70fa5c10fb2",
    "DEVICE_ID": [
      "b717f8d8-6f18-43c0-ae46-69c32998f653",
      "b717f8d8-6f18-43c0-ae46-69c32998f654"
    ],
    "STATUS": "SUCCESS"
  }
}
```

## DEVICE

### Thêm device vào mạng

1. Json mẫu

```json
{
  "CMD": "SCAN"
}
```

2. Giải thích

Thêm device vào mạng

3. Json phản hồi

```json
{
  "CMD": "TYPE_DEVICE",
  "DATA": {
    "DEVICE_ID": "b717f8d86f1843c0ae4669c32998f653",
    "DEVICE_UNICAST_ID": 2,
    "DEVICE_KEY": "b717f8d86f1843c0ae4669c32998f653",
    "NET_KEY": "b717f8d86f1843c0ae4669c32998f653",
    "APP_KEY": "b717f8d86f1843c0ae4669c32998f653",
    "CATEGORY_ID": 23002
  }
}
```

### Dừng quá trình đưa thiết bị vào mạng

1. Json mẫu

```json
{
  "CMD": "STOP"
}
```

2. Giải thích

Dừng quá trình đưa thiết bị vào mạng

3. Json phản hồi

```json
{
  "CMD": "STOP"
}
```

### Xóa device trong mạng

1. Json mẫu

```json
{
  "CMD": "RESET_NODE",
  "DATA": [
    "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "b717f8d8-6f18-43c0-ae46-69c32998f654"
  ]
}
```

2. Giải thích

Xóa device trong mạng. Từng device sẽ phản hồi về sau khi xóa khỏi mạng BLE

3. Json phản hồi

```json
{
  "CMD": "RESET_NODE",
  "DATA": {
    "DEVICE_ID": [
      "b717f8d8-6f18-43c0-ae46-69c32998f653",
      "b717f8d8-6f18-43c0-ae46-69c32998f654"
    ],
    "STATUS": "SUCCESS"
  }
}
```

## SCENE

### Gán cảnh cho device (công tắc cảnh hoặc cảm biến)

#### Gán cảnh cho cảm biến ánh sáng và cảm biến chuyển động

1. Json mẫu

```json
{
  "CMD": "SCENE_FOR_SENSOR_LIGHT_PIR",
  "TYPE": "CREATE",
  "DATA": {
    "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "EVENT_TRIGGER_TYPE_ID": 1,
    "LIGHT_SENSOR": {
      "LOW_LUX": 200,
      "HIGHT_LUX": 600,
      "COMPARISON_OPERATOR_ID": 7,
      "DEVICE_ATTRIBUTE_ID": 12
    },
    "PIR_SENSOR": {
      "PIR": 1,
      "COMPARISON_OPERATOR_ID": 1,
      "DEVICE_ATTRIBUTE_ID": 10
    }
  }
}
```

2. Giải thích

Thêm cảnh có EVENT_TRIGGER_ID: "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2" với điều kiện ánh sáng và điều kiện chuyển động cho cảm biến có 
"DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2"

3. Json phản hồi

```json
{
  "CMD": "SCENE_FOR_SENSOR_LIGHT_PIR",
  "DATA": {
    "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "LIGHT_SENSOR": {
      "LOW_LUX": 200,
      "HIGHT_LUX": 600,
      "COMPARISON_OPERATOR_ID": 7,
      "DEVICE_ATTRIBUTE_ID": 12
    },
    "PIR_SENSOR": {
      "PIR": 1,
      "COMPAIRISON_OPERATOR_ID": 1,
      "DEVICE_ATTRIBUTE_ID": 12
    }
  }
}
```

#### Gán cảnh cho nút nhấn của remote

1. Json mẫu

```json
{
  "CMD": "SCENE_FOR_REMOTE",
  "TYPE": "CREATE",
  "DATA": {
    "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "COMPARISON_OPERATOR_ID": 1,
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "DEVICE_ATTRIBUTE_ID": 11,
    "EVENT_TRIGGER_TYPE_ID": 1,
    "DEVICE_ATTRIBUTE_VALUE": {
      "BUTTON_VALUE": "BUTTON_1",
      "MODE_VALUE": 1
    }
  }
}
```

2. Giải thích

Gán cảnh cho nút nhấn số  1 trên remote AC và DC, với "DEVICE_ID":"aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2"

3. Json phản hồi

```json
{
  "CMD": "SCENE_FOR_REMOTE",
  "DATA": {
    "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "COMPARISON_OPERATOR_ID": 1,
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "DEVICE_ATTRIBUTE_ID": 11,
    "DEVICE_ATTRIBUTE_VALUE": {
      "BUTTON_VALUE": "BUTTON_1",
      "MODE_VALUE": 1
    }
  }
}
```

#### Gán cảnh cho màn hình

1. Json mẫu
```json
{
  "CMD": "SCENE_FOR_SCREEN",
  "TYPE": "CREATE",
  "DATA": [
    {
      "EVENT_TRIGGER_ID": "abc-cde",
      "EVENT_TRIGGER_NAME": "123",
      "EVENT_TRIGGER_ICON_FOR_SCREEN": 1
    },
    {
      "EVENT_TRIGGER_ID": "abc-cde",
      "EVENT_TRIGGER_NAME": "123",
      "EVENT_TRIGGER_ICON_FOR_SCREEN": 2
    }
  ]
}
```

2. Giải thích:
Đẩy cảnh cho màn hình hiển thị (EVENT_TRIGGER_NAME tối đa 10 ký tự)
3. Json phản hồi
```json
{
  "CMD": "SCENE_FOR_SCREEN",
  "DATA": {
    "EVENT_TRIGGER_ID": ["aa3549d4-5471-4d75-b0b2- b70fa5c10fb2","aa3549d4-5471-4d75-b0b2- b70fa5c10fb9"],
    "STATUS":"SUCCESS"
  }
}
```

### Sửa cảnh gán cho Device (công tắc cảnh hoặc cảm biến)

1. Json mẫu

```json
{
  "CMD": "SCENE_FOR_SENSOR_LIGHT_PIR",
  "TYPE": "EDIT",
  "DATA": {
    "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "LIGHT_SENSOR": {
      "LOW_LUX": 200,
      "HIGHT_LUX": 600,
      "COMPARISON_OPERATOR_ID": 7,
      "DEVICE_ATTRIBUTE_ID": 12
    },
    "PIR_SENSOR": {
      "PIR": 1,
      "COMPARISON_OPERATOR_ID": 1,
      "DEVICE_ATTRIBUTE_ID": 12
    }
  }
}
```

2. Giải thích

Sửa cảnh đã gán cho device có "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2"

3. Json phản hồi

```json
{
  "CMD": "SCENE_FOR_SENSOR_LIGHT_PIR",
  "DATA": {
    "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "LIGHT_SENSOR": {
      "LOW_LUX": 200,
      "HIGHT_LUX": 600,
      "COMPARISON_OPERATOR_ID": 7,
      "DEVICE_ATTRIBUTE_ID": 12
    },
    "PIR_SENSOR": {
      "PIR": 1,
      "COMPAIRISON_OPERATOR_ID": 1,
      "DEVICE_ATTRIBUTE_ID": 12
    }
  }
}
```

#### Sửa cảnh màn hình

1. Json mẫu
```json
{
  "CMD": "SCENE_FOR_SCREEN",
  "TYPE": "EDIT",
  "DATA": {
    "EDIT": [
      {
        "EVENT_TRIGGER_ID": "abc-cde",
        "EVENT_TRIGGER_NAME": "123",
        "EVENT_TRIGGER_ICON_FOR_SCREEN": 1
      },
      {
        "EVENT_TRIGGER_ID": "abc-cde",
        "EVENT_TRIGGER_NAME": "123",
        "EVENT_TRIGGER_ICON_FOR_SCREEN": 2
      }
    ],
    "ADD": [
      {
        "EVENT_TRIGGER_ID": "abc-cde",
        "EVENT_TRIGGER_NAME": "123",
        "EVENT_TRIGGER_ICON_FOR_SCREEN": 2
      }
    ],
    "DEL": [
      {
        "EVENT_TRIGGER_ID": "abc-cde"
      }
    ]
  }
}
```

2. Giải thích:
Sửa cảnh của màn hình (EVENT_TRIGGER_NAME tối đa 10 ký tự)
3. Json phản hồi
```json
{
  "CMD": "SCENE_FOR_SCREEN",
  "DATA": {
    "EVENT_TRIGGER_ID": ["aa3549d4-5471-4d75-b0b2- b70fa5c10fb2","aa3549d4-5471-4d75-b0b2- b70fa5c10fb9"],
    "STATUS":"SUCCESS"
  }
}
```

### Xóa cảnh gán với device (công tắc cảnh hoặc cảm biến)

1. Json mẫu

```json
{
  "CMD": "SCENE_FOR_REMOTE",
  "TYPE": "DELETE",
  "DATA": {
    "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "DEVICE_ATTRIBUTE_VALUE": {
      "BUTTON_VALUE": "BUTTON_1",
      "MODE_VALUE": 1
    }
  }
}
```

2. Giải thích

Xóa cảnh đã gán cho nút nhấn của remote

3. Json phản hồi

```json
{
  "CMD": "SCENE_FOR_REMOTE",
  "TYPE": "DELETE",
  "DATA": {
    "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
    "DEVICE_ATTRIBUTE_VALUE": {
      "BUTTON_VALUE": "BUTTON_1",
      "MODE_VALUE": 1
    }
  }
}
```

#### Xóa cảnh màn hình

1. Json mẫu
```json
{
  "CMD": "SCENE_FOR_SCREEN",
  "TYPE": "DELTE",
  "DATA": {
    "DEVICE_ID":"abc-cde"
  }
}
```

2. Giải thích:
Sửa cảnh của màn hình (EVENT_TRIGGER_NAME tối đa 10 ký tự)
3. Json phản hồi
```json
{
  "CMD": "SCENE_FOR_SCREEN",
  "DATA": {
    "EVENT_TRIGGER_ID": ["aa3549d4-5471-4d75-b0b2- b70fa5c10fb2","aa3549d4-5471-4d75-b0b2- b70fa5c10fb9"],
    "STATUS":"SUCCESS"
  }
}
```

### Tạo 1 EVEN TRIGGER

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
    "EACH_DAY": [
      "EACHMONDAY",
      "EACHTUESDAY"
    ],
    "DEVICES": [
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
        "PROPERTIES": [
          {
            "ID": 0,
            "VALUE": 1
          }
        ]
      }
    ]
  }
}
```

2. Giải thích

HC nhận được bản ghi thêm EvenTrigger sẽ lưu dữ liệu vào bảng EvenTrigger,kiểm tra trường EventTriggerTYPEID nếu bằng 1 (cảnh) thì sẽ gửi bản tin tạo cảnh xuống GateWay.

Lưu ý: VD: tạo SCENE không có thời gian thì bỏ các trường START_AT, END_AT, tạo  SCENE không có DEVICE bỏ trường DEVICE,....

3. Json phản hồi

```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "CREATE",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "SCENE_UNICAST_ID": 2,
    "EVENT_TRIGGER_TYPE_ID": 1,
    "STATUS": "SUCCESS"
  }
}
```

### Tạo 12 cảnh mặc định

1. Json mẫu
```json
{
  "CMD": "CREATE_DEFAULT_SCENES",
  "DATA": [
    {
      "SCENE_ID": "abcde",
      "DEVICES": [
        {
          "DEVICE_ID": "defghi",
          "PROPERTIES": [
            {
              "ID": 0,
              "VALUE": 1
            },
            {
              "ID": 1,
              "VALUE": 100
            }
          ]
        }
      ]
    },
    {
      "SCENE_ID": "abcxyz",
      "DEVICES": [
        {
          "DEVICE_ID": "defghi",
          "PROPERTIES": [
            {
              "ID": 0,
              "VALUE": 1
            },
            {
              "ID": 1,
              "VALUE": 100
            }
          ]
        }
      ]
    }
  ]
}
```

2. Giải thích:
Tạo 12 cảnh mặc định cho phòng
3. Json phản hồi (sau thời gian time out hc sẽ trả về cảnh nào vừa được cài đặt và trong cảnh đó có bao nhiêu thiết bị được cài thành công )

```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "CREATE",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "SCENE_UNICAST_ID": 2,
    "DEVICE_ID":["abc","cde"],
    "EVENT_TRIGGER_TYPE_ID": 1,
    "STATUS": "SUCCESS"
  }
}
```

### Sửa 1 EVEN TRIGGER

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
    "EACH_DAY": [
      "EACHMONDAY",
      "EACHTUESDAY"
    ],
    "DEVICES": [
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
        "TYPE": "EDIT",
        "PROPERTIES": [
          {
            "ID": 23,
            "VALUE": 6
          }
        ]
      },
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10f00",
        "TYPE": "DEL",
        "PROPERTIES": [
          {
            "ID": 23,
            "VALUE": 6
          }
        ]
      },
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10f00",
        "TYPE": "ADD",
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

HC nhận được bản tin sửa EVEN TRIGGER theo các thông số người dùng cài đặt (giống bản tin tạo event)nhưng thuộc tính "TYPE":"CREATE" được thay bằng "TYPE":"EDIT"

3. Json phản hồi

```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "EDIT",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "SCENE_UNICAST_ID": 2,
    "EVENT_TRIGGER_TYPE_ID": 1,
    "STATUS": "SUCCESS"
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
    "EVENT_TRIGGER_TYPE_ID": 1,
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2"
  }
}
```

2. Giải thích

Xóa 1 EVEN TRIGGER với ID tương ứng

3. Json phản hồi

```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "DELETE",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "SCENE_UNICAST_ID": 2,
    "EVENT_TRIGGER_TYPE_ID": 1,
    "STATUS": "SUCCESS"
  }
}
```

## BẢN TIN CẬP NHẬT TRẠNG THÁI THIẾT BỊ KHI VỪA MỞ APP

1. Json mẫu

```json
{
  "CMD": "DEVICE_UPDATE",
  "TIME_UPDATE":"YYYY MM D HH:MM"
}
```

2. Giải thích

Gửi bản tin yêu cầu báo cáo trạng thái hiện tại của các thiết bị

3. Json phản hồi

```json
{
  "CMD": "DEVICE_UPDATE",
  "DATA": {
    "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "ID": 0,
    "VALUE": 1
  }
}

{
  "CMD": "DEVICE_UPDATE",
  "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
  "STATUS":"OFFLINE"
  }
}
```

## RULE

### Tạo rule

1. Json mẫu

```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "CREATE",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "GROUP_ID": "97ab44a3-e788-46a1-9c07-79f39d6be33f",
    "EVENT_TRIGGER_TYPE_ID": 2,
    "PRIORITY": 3,
    "HAS_TIMER": 1,
    "START_AT": "10:56",
    "END_AT": "11:1",
    "HAS_REPEATER": 1,
    "EACH_DAY": [
      "EACHMONDAY",
      "EACHTUESDAY"
    ],
    "LOGICAL_OPERATOR_ID": 0,
    "STATUS_ID": 1,
    "INPUT_DEVICE": [
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
        "COMPARISON_OPERATOR_ID": 1,
        "DEVICE_ATTRIBUTE_ID": 11,
        "DEVICE_ATTRIBUTE_VALUE": 1
      },
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
        "COMPARISON_OPERATOR_ID": 1,
        "DEVICE_ATTRIBUTE_ID": 11,
        "DEVICE_ATTRIBUTE_VALUE": 1
      }
    ],
    "OUTPUT_DEVICE": {
      "DEVICES": [
        {
          "TYPE_RUN": 0,
          "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
          "PROPERTIES": [
            {
              "ID": 0,
              "VALUE": 1
            },
            {
              "ID": 2,
              "VALUE": 50
            }
          ]
        },
        {
          "TYPE_RUN": 0,
          "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb26666666666666",
          "PROPERTIES": [
            {
              "ID": 0,
              "VALUE": 1
            }
          ]
        }
      ],
      "GROUPS": [
        {
          "TYPE_RUN": 1,
          "GROUP_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
          "PROPERTIES": [
            {
              "ID": 0,
              "VALUE": 0
            }
          ]
        }
      ],
      "SCENE": [
        {
          "TYPE_RUN": 0,
          "SCENE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2"
        }
      ]
    }
  }
}
```

2. Giải thích

Tạo rule với các thông số được cài đặt theo thông số người dùng lựa chọn
*Lưu ý: VD: Nếu không có thời gian thì bỏ trường thời gian START_AT, END_AT

3. Json phản hồi

```json
{
  "CMD": "EVENT_TRIGGER",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "EVENT_TRIGGER_TYPE_ID": 2,
    "STATUS":"SUCCESS"
  }
}
```

### Sửa rule

1. Json mẫu

```json
{
  "CMD": "EVENT_TRIGGER",
  "TYPE": "EDIT",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "GROUP_ID": "97ab44a3-e788-46a1-9c07-79f39d6be33f",
    "EVENT_TRIGGER_TYPE_ID": 2,
    "PRIORITY": 3,
    "HAS_TIMER": 1,
    "START_AT": "10:56",
    "END_AT": "11:1",
    "HAS_REPEATER": 1,
    "EACH_DAY": [
      "EACHMONDAY",
      "EACHTUESDAY"
    ],
    "LOGICAL_OPERATOR_ID": 0,
    "STATUS_ID": 1,
    "INPUT_DEVICE": [
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
        "COMPARISON_OPERATOR_ID": 1,
        "DEVICE_ATTRIBUTE_ID": 11,
        "DEVICE_ATTRIBUTE_VALUE": 1
      },
      {
        "DEVICE_ID": "aa3549d4-5471-4d75-b0b2-  b70fa5c10fb2",
        "COMPARISON_OPERATOR_ID": 7,
        "DEVICE_ATTRIBUTE_ID": 9,
        "DEVICE_ATTRIBUTE_VALUE_LOW": 10,
        "DEVICE_ATTRIBUTE_VALUE_HIGHT": 100
      }
    ],
    "OUTPUT_DEVICE": {
      "DEVICES": [
        {
          "TYPE_RUN": 0,
          "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
          "PROPERTIES": [
            {
              "ID": 0,
              "VALUE": 1
            },
            {
              "ID": 2,
              "VALUE": 50
            }
          ]
        },
        {
          "TYPE_RUN": 0,
          "DEVICE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb26666666666666",
          "PROPERTIES": [
            {
              "ID": 0,
              "VALUE": 1
            }
          ]
        }
      ],
      "GROUPS": [
        {
          "TYPE_RUN": 1,
          "GROUP_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
          "PROPERTIES": [
            {
              "ID": 0,
              "VALUE": 0
            }
          ]
        }
      ],
      "SCENE": [
        {
          "TYPE_RUN": 0,
          "SCENE_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2"
        }
      ]
    }
  }
}
```

2. Giải thích

Giống bản tin tạo rule nhưng type là "EDIT" và các thông số  tất cả thông số của rule.

3. Json phản hồi

```json
{
  "CMD": "EVENT_TRIGGER",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "EVENT_TRIGGER_TYPE_ID": 2,
    "STATUS":"SUCCESS"
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
    "EVENT_TRIGGER_TYPE_ID": 1,
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2"
  }
}
```

2. Giải thích

Xóa rule đã tạo với ID tương ứng.

3. Json phản hồi

```json
{
  "CMD": "EVENT_TRIGGER",
  "DATA": {
    "EVENT_TRIGGER_ID": "aa3549d4-5471-4d75-b0b2- b70fa5c10fb2",
    "EVENT_TRIGGER_TYPE_ID": 2,
    "STATUS":"SUCCESS"
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

# MỘT SỐ BẢN TIN ĐẶC BIỆT

1. Bản tin phản hồi khi thiết bị được thêm vào mạng

```json
{
  "CMD": "TYPE_DEVICE",
  "DATA": {
    "DEVICE_UNICAST_ID": 123,
    "DEVICE_ID": "b717f8d86f1843c0ae4669c32998f653",
    "DEVICE_KEY": "b717f8d86f1843c0ae4669c32998f653",
    "NET_KEY": "b717f8d86f1843c0ae4669c32998f653",
    "APP_KEY": "b717f8d86f1843c0ae4669c32998f653",
    "DEVICE_TYPE_ID": 23002
  }
}
```

2. Bản tin phản hồi thiệt độ, độ ẩm, bụi mịn :2.5;10;1.0

```json
{
  "CMD": "PM_SENSOR",
  "DATA": {
    "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "TEMPERATURE_VALUE": 30,
    "HUMIDITY_VALUE": 30
  }
}

{
  "CMD": "PM_SENSOR",
  "DATA": {
    "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "PM2.5_VALUE": 30,
    "PM1_VALUE": 30,
    "PM10_VALUE": 30
  }
}
```

3. Bản tin phản hồi pin, lux, pir

```json
{
  "CMD":"POW_STATUS",
  "DATA":{
    "DEVICE_ID":"b717f8d8-6f18-43c0-ae46-69c32998f653",
    "POWER_VALUE":30
  }
}

{
  "CMD":"LIGHT_SENSOR",
  "DATA":{
    "DEVICE_ID":"b717f8d8-6f18-43c0-ae46-69c32998f653",
    "LUX_VALUE":30
  }
}

{
  "CMD":"PIR_SENSOR",
  "DATA":{
    "DEVICE_ID":"b717f8d8-6f18-43c0-ae46-69c32998f653",
    "PIR_VALUE":30
  }
}
```

4. Bản tin phản hồi trạng thái nút nhấn

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

5. Bản tin phản hồi trạng thái cảm biến khói

```json
{
  "CMD": "SMOKE_SENSOR",
  "DATA": {
    "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "SMOKE_VALUE":1
  }
}


{
  "CMD": "SMOKE_SENSOR",
  "DATA": {
    "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "SMOKE_POWER":"LOW_BATTERY"
  }
}
```

6. Bản tin phản hồi cảm biến cửa

```json
{
  "CMD": "DOOR_SENSOR",
  "DATA": {
    "DEVICE_ID": "b717f8d8-6f18-43c0-ae46-69c32998f653",
    "HANG_VALUE":1,
    "DOOR_VALUE":1
  }
}
```
