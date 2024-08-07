# SyntheticData

Библиотека «SyntheticData» представляет собой класс с набором методов и функций для моделирования геодезических сетей, временных рядов решений Precise Point Positioning (PPP), внесения аномалий в измерения, преобразования координат между различными системами, а также набором инструментов для визуализации и упаковки смоделированных данных в файл формата «DataFrame». 

## **Класс SyntheticData (`Synthetic_Data.py`)**

Класс `SyntheticData` содержит следующие методы:

### Методы

#### `my_geodetic2ecef(df)`

Конвертирует координаты из системы BLH в XYZ.

#### `my_ecef2geodetic(df)`

Конвертирует координаты из системы XYZ в BLH.

#### `unique_names(df)`

Возвращает список уникальных имен станций в DataFrame.

#### `random_points(B, L, H, zone, amount, method, min_dist, max_dist)`

Генерирует случайную сеть пунктов с заданными параметрами.

#### `triangulation(df, subplot, canvas, max_baseline)`

Строит геодезическую сеть триангуляции и рисует ее на графике.

#### `create_dataframe(df, date_list)`

Заполняет DataFrame координатами для каждой даты и каждого геодезического пункта.

#### `harmonics(df, date_list, periods_in_year)`

Добавляет годовые и полугодовые колебания к координатам.

#### `linear_trend(df, date_list, periods_in_year)`

Добавляет линейный тренд к координатам.

#### `noise(df, num_periods)`

Добавляет шум к координатам.

#### `impulse(df, impulse_size, target_date=None, num_stations=1, random_dates=0)`

Добавляет импульс к координатам.

## **Пример использования**

```python
synthetic_data = SyntheticData() 
df = synthetic_data.random_points(B=50, L=100, H=200, zone=10, amount=10, method='consistent', min_dist=5, max_dist=20) 
df = synthetic_data.create_dataframe(df, date_list=['2020-01-01', '2020-01-02', ...]) 
df = synthetic_data.harmonics(df, date_list, periods_in_year=365) 
df = synthetic_data.linear_trend(df, date_list, periods_in_year=365) 
df = synthetic_data.noise(df, num_periods=100) 
df = synthetic_data.impulse(df, impulse_size=0.1, target_date='2020-01-01', num_stations=1) 
```

# Класс Tests (`congruency.py`)

Класс предназначен для выполнения геометрического теста конгруэнтности геодезической сети. Тест позволяет определить, является ли геодезическая сеть конгруэнтной на начальную и i-ую эпохи. 
Конгруэнтность проверяется при помощи T-теста (ttest) и теста Хи-квадрат (chi2).
Для проведения теста необходимо импортировать файл формата .csv или DataFrame.

### Функциональность

Код реализует два метода теста конгруэнтности:

-   Метод, основанный на вычислении разностей базовых линий на разные эпохи (`line_based`)
-   Метод, основанный на вычислении разностей координат пунктов на разные эпохи (`coordinate_based`)

### Использование

Пример использования:
```python
import pandas as pd
df = pd.read_csv('your_file.csv', delimiter=';')
test = Tests(df)
test.congruency_test(df=df, method='coordinate_based')
```

## Файл `main_interface.py`

Данный файл содержит код Qt-интерфейса для оконного приложения, написанного при помощи библиотеки PySide и Matplotlib

## **Автор**

Артем Маликов 
a.o.malikov@mail.ru
