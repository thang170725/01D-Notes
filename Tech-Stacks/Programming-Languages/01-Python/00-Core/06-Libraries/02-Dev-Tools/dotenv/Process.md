- [load\_dotenv()](#load_dotenv)
---
# load_dotenv()
```python
from dotenv import load_dotenv
import os

load_dotenv()
DATABASE_URL = os.getenv("DATABASE_URL", default="Empty")

print(DATABASE_URL) # mysql+pymysql://ai_user:ai123@localhost:3306/SmartRecipe
```
