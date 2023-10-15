# Chapter 2: note and summary part 2

## Chat Completion

Tham khảo: [https://platform.openai.com/docs/api-reference/chat](https://platform.openai.com/docs/api-reference/chat) để hiểu hơn code. 

Chúng ta có thể custom cái chat completion với các role khác nhau. 

Nghĩa là cung cấp context cho gpt rõ ràng hơn để đưa ra kết quả mong muốn. 

Ví dụ với setup bên dưới. Bạn đưa ra vai trò của con chat (system) và các ví dụ (cho vào assistant) để nó biết ngõ bắt chước theo. 

```python
import openai
import os
from dotenv import load_dotenv
load_dotenv()

openai.api_key = os.getenv("OPENAI_API_KEY")

response = openai.ChatCompletion.create(
    model = "gpt-3.5-turbo",
    messages = [
        {"role": "system", "content": "You are a helpful teacher."},
        {
            "role": "user",
            "content": "Are there other measures than time complexity for an \
                algorithm?",
        },

        {
            "role": "assistant",
            "content": "Yes, there are other measures besides time complexity \
                for an algorithm, such as space complexity.",

        },

        {"role": "user", "content": "What is it?"},
    ]
)

print(response["choices"][0]["message"]["content"])
```

**Output:**

```python
Space complexity refers to the amount of memory or space required by an algorithm to solve a problem. It measures the maximum amount of memory space that an algorithm requires at any given point during its execution.

This can be further classified into two types:

1. Auxiliary Space Complexity: It refers to the space required by an algorithm, excluding the input and output space. It includes the extra space used by the algorithm for variables, temporary data structures, recursion stack, etc.

2. Total Space Complexity: It refers to the total space required by an algorithm, including both the input and output space as well as the auxiliary space. It takes into account the space required by the algorithm throughout its entire execution, from the initial presentation of the input to the final presentation of the output.

Similar to time complexity, space complexity is also expressed using Big O notation to indicate the upper bound on space usage as the input size increases. The common notations used are O(1) for constant space, O(n) for linear space, O(n^2) for quadratic space, and so on.

Considering both time and space complexity helps in analyzing and comparing the efficiency of different algorithms and choosing the most suitable one for a given problem.
```

Còn khi ta muốn đưa ra format phù hợp hơn. 

Ta thêm vào chỗ system: “**You're very concise about what you say. Only response with one short sentence in simple language**” (trả lời ngắn gọn trong vòng một câu là xong)

```python
import openai
import os
from dotenv import load_dotenv
load_dotenv()

openai.api_key = os.getenv("OPENAI_API_KEY")

response = openai.ChatCompletion.create(
    model = "gpt-3.5-turbo",
    messages = [
        {"role": "system", "content": "You are a helpful teacher. \
         You're very concise about what you say. Only response with one short sentence in simple language"},
        {
            "role": "user",
            "content": "Are there other measures than time complexity for an \
                algorithm?",
        },

        {
            "role": "assistant",
            "content": "Yes, there are other measures besides time complexity \
                for an algorithm, such as space complexity.",

        },

        {"role": "user", "content": "What is it?"},
    ]
)

print(response["choices"][0]["message"]["content"])
```

Output:

```python
Space complexity refers to the amount of memory or storage required by an algorithm to solve a problem.
```