# 修改说明[Changelog]

## 2024年6月1日

- 【功能：修改】网页标题LOGO更换

  ChuanhuChatbot.py Line 815

  ```
  demo.title = i18n("HooChat 🚀")
  ```

- 【功能：修改】左侧边栏LOGO更换

  modules/presets.py Line 50

  ```
  CHUANHU_TITLE = i18n("HooChat 🚀")
  ```

## 2024年5月31日

- 【BUG】ERNIE、Claude模型下，所有用户的聊天记录是互相可见的

  - ChuanhuChatbot.py  Line 516，本来传入了user_name，但在get_model中ERNIE、Claude没有接收这个变量

  - modules/models/ERNIE.py Line 8，12 增加 user_name入参和成员变量赋值
  
      ```
      class ERNIE_Client(BaseLLMModel):
          def __init__(self, model_name, api_key, secret_key, user_name) -> None:
              super().__init__(model_name=model_name)
              self.api_key = api_key
              self.api_secret = secret_key
              self.user_name = user_name
      ```
  
  - modules/models/Claude.py Line 9, 12 增加 user_name入参和成员变量赋值
  
    ```
    class Claude_Client(BaseLLMModel):
        def __init__(self, model_name, api_secret, user_name) -> None:
            super().__init__(model_name=model_name)
            self.api_secret = api_secret
            self.user_name = user_name
    ```
  


## 2024年5月30日

- 【功能：新增】增加对ERNIE Speed 8K/128K免费API的支持
  - modules/presets.py Line 55，增加两个新API：ERNIE-Speed-8K和ERNIE-Speed-128K
  
    ```
    ONLINE_MODELS = [
        "ERNIE-Speed-8K",
        "ERNIE-Speed-128K",
        "GPT3.5 Turbo",
        "GPT-4o",
    ```
  
  - modules/presets.py Line 139，315+ 增加两个新API的模型描述
  
    ```
    # Additional metadata for online and local models
    MODEL_METADATA = {
        "ERNIE-Speed-8K": {
            "model_name": "ERNIE-Speed-8K",
            "token_limit": 8192,
        },
        "ERNIE-Speed-128K": {
            "model_name": "ERNIE-Speed-128K",
            "token_limit": 131072,
        }
    ```
  
  - modules/models/ERNIE.py Line 22 增加两个API的调用URL
  
    ```
    elif self.model_name == "ERNIE-Speed-8K":
        self.ERNIE_url = "https://aip.baidubce.com/rpc/2.0/ai_custom/v1/wenxinworkshop/chat/ernie_speed?access_token="
    elif self.model_name == "ERNIE-Speed-128K":
        self.ERNIE_url = "https://aip.baidubce.com/rpc/2.0/ai_custom/v1/wenxinworkshop/chat/ernie-speed-128k?access_token="
    ```

- 【配置：使用】用户自定义配置

  - 创建新的config.json文件，注意只放入需要修改的key, value，不要直接那config_example.json复制，因为多余的条目会出问题

    ```
    {
        "ernie_api_key": "xxx",
        "ernie_secret_key": "xxx",
        "local_embedding": true,
        "users": [["adas1","12345"],["jack2","12345"]],
        "default_model": "ERNIE-Speed-8K"
    }
    ```
