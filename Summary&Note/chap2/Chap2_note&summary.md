# Chapter 2: Note and summary 

# Hello world

Trong chapter 2 chúng ta làm quen sử dụng Open AI API. 

Tất cả các ví dụ trong sách sẽ trong link github này:

[GitHub - malywut/gpt_examples](https://github.com/malywut/gpt_examples/tree/main)

Để hiểu code ta tra cứu ở đây:

[OpenAI Platform](https://platform.openai.com/docs)

Chúng ta sẽ viết chương trình “Hello world” phiên bản gpt.

### Nguyên tắc cốt lõi

Phương thức lập trình sẽ là tương tác với gpt bằng **prompt** để nó đưa ra kết quả ta mong muốn. 

![Untitled](Chapter%202%20Note%20and%20summary%209720c616522a41faa18ad3f849c3241f/Untitled.png)

![Untitled](Chapter%202%20Note%20and%20summary%209720c616522a41faa18ad3f849c3241f/Untitled%201.png)

### Chọn model

Lựa chọn nhiều nhất là **gpt-3.5-turbo** đã được cải thiện hơn nhiều và rẻ hơn 50 lần so với **gpt4** thời điểm hiện tại

Khi đó ta sẽ chọn ở trong code là: 

```jsx
model="gpt-3.5-turbo"
```

### Dùng API

**Lấy API key:** 

Vào [https://platform.openai.com/](https://platform.openai.com/) và lấy API key thôi. 

![Untitled](Chapter%202%20Note%20and%20summary%209720c616522a41faa18ad3f849c3241f/Untitled%202.png)

Nếu bạn nào chưa có thì có thể đăng ký với Open AI hoặc mua tài khoản bên ngoài có cung cấp cho mình API để dùng. 

Nên nhớ bảo mật nếu không muốn bị hao $$$ 

Nên ta phải setup môi trường: 

### Setup môi trường

Bạn sẽ bỏ hết secret key của mình vào file **.env** trong như này:

![Untitled](Chapter%202%20Note%20and%20summary%209720c616522a41faa18ad3f849c3241f/Untitled%203.png)

Và gọi lên như này: 

```jsx
import openai
import os
from dotenv import load_dotenv

load_dotenv()
openai.api_key = os.getenv("OPENAI_API_KEY")

```

### Hello world:

Nhớ setup môi trường (tham khảo link github ở đầu trang, tham khảo file **requirements.txt)**

```python
pip install openai python-dotenv
```

.env

![Untitled](Chapter%202%20Note%20and%20summary%209720c616522a41faa18ad3f849c3241f/Untitled%204.png)

Chương trình Hello world sẽ như sau: 

[run.py](http://run.py) 

```python
from dotenv import load_dotenv

load_dotenv()
import os
import openai

openai.api_key = os.getenv("OPENAI_API_KEY")

# Call the openai ChatCompletion endpoint, with th ChatGPT model
response = openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
        {"role": "user", "content": "Hello World!"}
    ]
)

# Extract the response
print(response['choices'][0]['message']['content'])
```

Output:

![Untitled](Chapter%202%20Note%20and%20summary%209720c616522a41faa18ad3f849c3241f/Untitled%205.png)

### Nếu muốn đưa ra output hay hơn thì ta tuỳ chỉnh prompt

Ví dụ như của mình muốn nó đáp lại như một nhân vật phản diện: 

Prompt của mình:

**You're a villain in a game. You will respond the way a villain would. But be concise about what you say. Now I say: Hello world!**

Code:

```python
from dotenv import load_dotenv

load_dotenv()
import os
import openai

openai.api_key = os.getenv("OPENAI_API_KEY")

# Call the openai ChatCompletion endpoint, with th ChatGPT model
response = openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
        {"role": "user", "content": "You're a villain in a game. You will respond the way a villain would. But be concise about what you say. Now I say: Hello world!"}
    ]
)

# Extract the response
print(response['choices'][0]['message']['content'])
```

Output

![Untitled](Chapter%202%20Note%20and%20summary%209720c616522a41faa18ad3f849c3241f/Untitled%206.png)