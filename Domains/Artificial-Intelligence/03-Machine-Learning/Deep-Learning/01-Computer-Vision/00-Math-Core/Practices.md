- [Demo cách hoạt động của BatchNorm](#demo-cách-hoạt-động-của-batchnorm)
---
# Demo cách hoạt động của BatchNorm
```python
import numpy as np

def batchnorm(x, eps=1e-5):
    # x: (N, H, W, C)
    
    # mean theo channel
    mean = np.mean(x, axis=(0,1,2), keepdims=True)
    
    # variance theo channel
    var = np.var(x, axis=(0,1,2), keepdims=True)
    
    # normalize
    x_hat = (x - mean) / np.sqrt(var + eps)
    
    # gamma, beta (giả sử =1,0)
    gamma = np.ones_like(mean)
    beta = np.zeros_like(mean)
    
    out = gamma * x_hat + beta
    
    return out
```