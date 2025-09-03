# Flask API 文档

本项目提供了用户与管理员的登录、注册、聊天、个人信息等接口。

------------------------------------------------------------------------

## 🔑 用户认证接口

### 1. 用户注册

-   **URL**: `/api/register`

-   **方法**: `POST`

-   **参数**:

    ``` json
    {
      "username": "用户名",
      "password": "密码",
      "email": "邮箱",
      "captcha": "验证码"
    }
    ```

-   **返回**:

    ``` json
    {
      "success": true,
      "message": "注册成功",
      "user_uuid": "唯一用户ID"
    }
    ```

### 2. 用户登录

-   **URL**: `/api/login`

-   **方法**: `POST`

-   **参数**:

    ``` json
    {
      "username": "用户名",
      "password": "密码",
      "captcha": "验证码",
      "remember": true
    }
    ```

-   **返回**:

    ``` json
    {
      "success": true,
      "message": "登录成功",
      "username": "用户名",
      "token": "JWT令牌"
    }
    ```

### 3. 用户登出

-   **URL**: `/api/logout`

-   **方法**: `POST`

-   **返回**:

    ``` json
    {
      "success": true,
      "message": "登出成功",
      "uuid": "用户ID"
    }
    ```

### 4. 获取验证码

-   **URL**:
    -   注册验证码: `/api/register/captcha`
    -   登录验证码: `/api/login/captcha`
-   **方法**: `GET`
-   **返回**: PNG图片（二进制流）

------------------------------------------------------------------------

## 💬 聊天接口

### 1. 发送消息并获取回复

-   **URL**: `/api/chat/get_response`

-   **方法**: `POST`

-   **参数**:

    ``` json
    {
      "text": "用户输入",
      "topic_id": "话题ID(可选),第一次不用携带"
    }
    ```

-   **返回**:

    ``` json
    {
      "success": true,
      "reply": "AI回答",
      "topic_id": "话题ID"
    }
    ```

### 2. 开启新话题

-   **URL**: `/api/chat/update_chat`

-   **方法**: `POST`

-   **参数**:

    ``` json
    { "new": true }
    ```

-   **返回**:

    ``` json
    {
      "success": true,
      "message": "新话题已开始",
      "topic_id": "话题ID",
      "chat_history": [
        {"role": "system", "content": "You are a helpful assistant"}
      ]
    }
    ```

### 3. 获取用户所有历史对话

-   **URL**: `/api/chat/history_response`

-   **方法**: `POST`

-   **参数**:

    ``` json
    { "user_uuid": "用户ID" }
    ```

-   **返回示例**:

    ``` json
    {
      "history": [
        {
          "topic_id": "123456",
          "user_question": {
            "role": "user",
            "content": "你好"
          },
          "assistant_reply": {
            "role": "assistant",
            "content": "你好，我能帮你什么？"
          }
        },
        {
          "topic_id": "654321",
          "user_question": {
            "role": "user",
            "content": "帮我写个Python代码"
          },
          "assistant_reply": {
            "role": "assistant",
            "content": "好的，这里是示例代码..."
          }
        }
      ]
    }
    ```

### 4. 获取某一话题的完整对话

-   **URL**: `/api/chat/Specific_history`

-   **方法**: `POST`

-   **参数**:

    ``` json
    {
      "user_uuid": "用户ID",
      "topic_id": "话题ID"
    }
    ```

-   **返回示例**:

    ``` json
    {
      "reply": [
        { "role": "user", "content": "你好" },
        { "role": "assistant", "content": "你好，我能帮你什么？" },
        { "role": "user", "content": "给我解释下Flask是什么" },
        { "role": "assistant", "content": "Flask 是一个 Python Web 框架..." }
      ]
    }
    ```

------------------------------------------------------------------------

## 👤 用户信息接口

### 1. 获取当前用户信息

-   **URL**: `/api/get_info/user`

-   **方法**: `POST`

-   **返回**:

    ``` json
    {
      "success": true,
      "message": "用户信息查询成功",
      "data": {
        "user_id": "用户ID",
        "username": "用户名",
        "email": "邮箱"
      }
    }
    ```

------------------------------------------------------------------------

## 👨‍💼 管理员接口

### 1. 管理员登录

-   **URL**: `/api/login/admin`

-   **方法**: `POST`

-   **参数**:

    ``` json
    {
      "Admin_name": "管理员用户名",
      "password": "密码"
    }
    ```

### 2. 创建管理员

-   **URL**: `/api/creat_info/admin`

-   **方法**: `POST`

-   **参数**:

    ``` json
    {
      "username": "管理员用户名",
      "password": "密码"
    }
    ```

### 3. 获取管理员信息

-   **URL**: `/api/get_info/admin`

-   **方法**: `POST`

-   **参数**:

    ``` json
    { "Admin_name": "管理员用户名" }
    ```

------------------------------------------------------------------------

## ⚙️ 日志

-   日志文件路径：`logs/app.log`
-   控制台与文件同时输出
-   最大大小：5MB，保留 5 个备份

------------------------------------------------------------------------

## 🚀 启动方式

``` bash
python app.py
```

服务启动后默认运行在: `http://0.0.0.0:5000`
