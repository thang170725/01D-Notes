- [Thuật toán](#thuật-toán)
- [Data](#data)
- [Build tree](#build-tree)
- [Predict](#predict)
---
# Demo research thuật toán decision tree
```python
import numpy as np

def entropy(y):
    counts = np.bincount(y)
    probs = counts / len(y)
    ent = 0
    for p in probs:
        if p > 0:
            ent -= p * np.log2(p)
    return ent

def best_split(X, y):
    m, n = X.shape
    base_entropy = entropy(y)
    best_gain = 0
    best_feature = None
    best_threshold = None

    for feature in range(n):
        values = np.unique(X[:, feature])
        for threshold in values:
            left_mask = X[:, feature] <= threshold
            right_mask = X[:, feature] > threshold

            if sum(left_mask) == 0 or sum(right_mask) == 0:
                continue

            left_entropy = entropy(y[left_mask])
            right_entropy = entropy(y[right_mask])
            weighted_entropy = (sum(left_mask) * left_entropy + sum(right_mask) * right_entropy) / m

            info_gain = base_entropy - weighted_entropy

            print(f"Feature {feature}, Threshold {threshold}, Info Gain {info_gain:.4f}")

            if info_gain > best_gain:
                best_gain = info_gain
                best_feature = feature
                best_threshold = threshold

    return best_feature, best_threshold

def build_tree(X, y, depth=0, max_depth=2):
    if len(set(y)) == 1:
        return {'leaf': True, 'class': y[0]}
    if depth >= max_depth:
        counts = np.bincount(y)
        return {'leaf': True, 'class': np.argmax(counts)}

    feature, threshold = best_split(X, y)
    if feature is None:
        counts = np.bincount(y)
        return {'leaf': True, 'class': np.argmax(counts)}

    left_mask = X[:, feature] <= threshold
    right_mask = X[:, feature] > threshold

    left_subtree = build_tree(X[left_mask], y[left_mask], depth + 1, max_depth)
    right_subtree = build_tree(X[right_mask], y[right_mask], depth + 1, max_depth)

    return {
        'leaf': False,
        'feature': feature,
        'threshold': threshold,
        'left': left_subtree,
        'right': right_subtree
    }

def predict_one(x, tree):
    if tree['leaf']:
        return tree['class']
    if x[tree['feature']] <= tree['threshold']:
        return predict_one(x, tree['left'])
    else:
        return predict_one(x, tree['right'])

def predict(X, tree):
    return np.array([predict_one(x, tree) for x in X])

# Data
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([0, 0, 1, 1, 1])

# Build tree
tree = build_tree(X, y, max_depth=2)

# Predict
print(predict(np.array([[1.5], [3.5], [4.5]]), tree))
# Feature 0, Threshold 1, Info Gain 0.3219
# Feature 0, Threshold 2, Info Gain 0.9710
# Feature 0, Threshold 3, Info Gain 0.4200
# Feature 0, Threshold 4, Info Gain 0.1710
[0 1 1]
```