# fit & transform trong xử lý dữ liệu
```python
class SimpleCleaner:
    def fit(self, df):
        self.score_median = df['score'].median()
        return self

    def transform(self, df):
        df = df.copy()
        df['invalid_score'] = (df['score'] > 100).astype(int)
        df['score'] = df['score'].fillna(self.score_median)
        return df
```