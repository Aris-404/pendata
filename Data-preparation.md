# Data Preparation

## Tugas

1. Missing values : menyelesaikan dengan WKNN (manual) + code menghitung WKNN
2. Normalisasi data (materi)
    - macam macam normalisasi data dan beri contoh hasil normalisasi data
    - Gunakan library sklearn untuk melakukan normalisasi data atau membuat fungsi sendiri

Penyelesaian:

| Data | Berat Badan (x) | Tinggi badan (y)  |
| ---- | --------------- | ----------------- |
| 1    | 50              | 150               |
| 2    | 65              | 160               |
| 3    | 80              | 170               |
| 4    | ?               | 165               |

### 1. Menyelesaikan Missing Values dengan WKNN

#### Manual

| Tetangga | Selisih (yi - yj) | Jarak (d) | Bobot (w)     |
| -------- | ----------------- | --------- | ------------- |
| 1        | (165 - 150) = 15  | 15        | 1/15 = 0.067  |
| 2        | (165 - 160) = -5  | 5         | 1/5 = 0.2     |
| 3        | (165 - 170) = 5   | 5         | 1/5 = 0.2     |

Pembilang:

| Data  | Bobot (w) \* Nilai (xj) |
| ----- | ----------------------- |
| 1     | 0.067 * 50 ≈ 3.35       |
| 2     | 0.2 * 65 = 13           |
| 3     | 0.2 * 80 = 16           |
| Total | 32.35                   |

Penyebut:

| Data  | Bobot (w) |
| ----- | --------- |
| 1     | 0.067     |
| 2     | 0.2       |
| 3     | 0.2       |
| Total | 0.467     |

```
x4 = Pembilang / Penyebut
x4 = 32.35 / 0.467
x4 = 69.27
```

#### Code Menghitung WKNN

```python
import numpy as np

# Data
data = np.array([[50, 150], [65, 160], [80, 170], [np.nan, 165]])

# Hitung jarak (berdasarkan tinggi badan)
distances = np.abs(data[:, 1] - data[3, 1])

# Bobot (inverse distance)
weights = 1 / (distances + 1e-5)

# Hitung missing value
missing_value = np.sum(weights[:-1] * data[:-1, 0]) / np.sum(weights[:-1])

print(missing_value)
```

### 2. Normalisasi Data

Normalisasi data adalah proses mengubah nilai-nilai dalam dataset ke dalam skala yang sama. Ada beberapa metode normalisasi data, di antaranya:

- Min-Max Normalization: Mengubah nilai ke dalam rentang [0, 1].
- Z-Score Normalization: Mengubah nilai berdasarkan rata-rata dan standar deviasi.

#### Min-Max Normalization

Manual:

| Data | Berat Badan (x) | Tinggi Badan (y) | Normalisasi (x')            | Normalisasi (y')         |
| ---- | --------------- | ---------------- | --------------------------- | ------------------------ |
| 1    | 50              | 150              | (50 - 50) / (80 - 50) = 0.0 | (150-150)/(170-150)=0.0  |
| 2    | 65              | 160              | (90 - 50) / (80 - 50) = 0.5 | (160-150)/(170-150)=0.5  |
| 3    | 80              | 170              | (80 - 50) / (80 - 50) = 1.0 | (170-150)/(170-150)=1.0  |
| 4    | ?               | 165              | ?                           | (165-150)/(170-150)=0.75 |

Code menggunakan sklearn:

```python
from sklearn.preprocessing import MinMaxScaler
import numpy as np

data = np.array([[50, 150], [65, 160], [80, 170], [np.nan, 165]])

scaler = MinMaxScaler()
normalized_data = scaler.fit_transform(data)

print(normalized_data)
```

#### Z-Score Normalization

Manual:

```
Rata-rata (mean) untuk x = (50 + 65 + 80) / 3
                         = 65
Standar deviasi (std) untuk x = sqrt(((50-65)^2 + (65-65)^2 + (80-65)^2)/3)
                              = sqrt((225 + 0 + 225)/3)
                              = sqrt(150)
                              = 12.25
Rata-rata (mean) untuk y = (150 + 160 + 170 + 165) / 4
                         = 161.25
Standar deviasi (std) untuk y = sqrt(((150-161.25)^2 + (160-161.25)^2 + (170-161.25)^2 + (165-161.25)^2)/4)
                              = sqrt((126.56 + 1.56 + 76.56 + 14.06)/4)
                              = sqrt(54.69)
                              = 7.39
```

| Data | Berat Badan (x) | Tinggi Badan (y) | Normalisasi (x')         | Normalisasi (y')           |
| ---- | --------------- | ---------------- | ------------------------ | -------------------------- |
| 1    | 50              | 150              | (50-65)/12.25 = -1.22    | (150-161.25)/7.39 = -1.52  |
| 2    | 65              | 160              | 0                        | (160-161.25)/7.39 = -0.17  |
| 3    | 80              | 170              | 1.22                     | (170-161.25)/7.39 = 1.18   |
| 4    | ?               | 165              | ?                        | (165-161.25)/7.39 = 0.51   |

Code menggunakan sklearn:

```python
from sklearn.preprocessing import StandardScaler
import numpy as np

data = np.array([[50, 150], [65, 160], [80, 170], [np.nan, 165]])

scaler = StandardScaler()
normalized_data = scaler.fit_transform(data)

print(normalized_data)
```