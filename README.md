# API 设计规范

## REST API

1. 使用 REST 风格的接口，无特殊情况下使用 JSON 当作返回值
2. 使用 GET 获取数据、PUT 修改、上传数据、POST 新增数据、DELETE 删除数据
3. 在 HTTP Response 中使用正确的状态码，如 2xx, 4xx, 5xx 等

## 版本化

1.在设计之初就进行版本化，在同一版本中，接口的返回形式不能够改变，版本化后 URL 如:

`https://api.gagogroup.cn/api/v1`

## JSON 格式规范

1. 如果接口返回正确的值应为:

```JSON
"data": {
  "content": "content goes for here"
}
"code":18721
```

其中，data 内包含正确情况下返回的 Object，code 为业务层状态码 (非 HTTP 状态码)

如果错误应该返回:

```JSON
"error": {
  "code": 400,
  "message": "USERNAME_OR_PASSWORD_ERROR"
}
```

或

```JSON
"errors": [
  {
    "code": 400,
    "message": "argument 0 should be a number"
  },
  {
    "code": 400,
    "message": "argument 1 should be a string"
  }
]
```

2. JSON 的 key 需要使用首字母小写的驼峰命名法，如:

```JSON
{
  "propertyName": "propertyValue"
}
```

3. JSON 中不应该包含任何注释
4. JSON 中如果该值是一个数组应当用复数的英文单词，如:

```JSON
{
  "siblings": ["bart", "maggie"]
}
```

5. 应当用 string 类型表示 enum，如:

```JSON
{
  "colors": ["WHITE", "BLACK"]
}
```

6. 使用 RFC 3339 或者 Unix Timestamp 来表示时间点，如:

```JSON
{
  "lastUpdate": "2007-11-06T16:34:41.000Z"
}

{
  "lastUpdateAt": 1477549002
}
```

**请注意，Unix Timestamp 只有10位的，13位的叫做毫秒**

7. 使用 ISO 8601 标准来表示持续时间

如: three years, six months, four days, twelve hours, thirty minutes, and five seconds

```JSON
{
  "duration": "P3Y6M4DT12H30M5S"
}
```

8. 在修改(PUT)或新增(POST)的接口成功后，应考虑返回 Object ID 或者完整的 Object

如，修改用户信息即 PUT /user 成功后应返回:

```JSON
{
  "uid": 198211
}
```

或

```JSON
{
  "uid": 198211,
  "username": "gago_user",
  "displayName": "小康"
}
```
