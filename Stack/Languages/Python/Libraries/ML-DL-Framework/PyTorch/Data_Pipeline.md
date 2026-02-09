mport Dataset
import pandas as pd
from typing import List

class RealEstateDataset(Dataset):
    def __init__(self, 
        data_frame: pd.DataFrame, 
        features: List[str],
        label: List[str]) -> None:

        self.data = data_frame

        self.X = torch.tensor(
            self.data[features].to_numpy(), 
            dtype=torch.float32
        )
        self.y = torch.tensor(
            self.data[label].to_numpy(), 
            dtype=torch.float32
        )
    
    def __len__(self) -> int:
        return len(self.data)
    
    def __getitem__(self, idx) -> tuple:
        return self.X[idx], self.y[idx]
    
if __name__ == "__main__":
    data = {
        'size': [850, 900, 1200, 1500],
        'bedrooms': [2, 3, 3, 4],
        'age': [10, 15, 20, 5],
        'price': [200000, 250000, 300000, 350000]
    }

    df = pd.DataFrame(data)
    
    features = ['size', 'bedrooms', 'age']
    labels = ['price']

    dataset = RealEstateDataset(df, features, labels)
    print(f'Data length: {dataset.__len__()}')
    print(f'First sample: {dataset.__getitem__(0)}')
Data length: 4
First sample: (tensor([850.,   2.,  10.]), tensor([200000.]))