# Kicksharing EDA

*Exploratory Data Analysis of Russian kicksharing trips*


## Оглавление

- [Описание проекта](#описание-проекта)
- [Данные](#данные)
- [Ключевые шаги анализа](#ключевые-шаги-анализа)
- [Основные выводы](#основные-выводы)
- [Как запустить](#как-запустить)

## Описание проекта

В репозитории собран EDA датасета сервиса проката электросамокатов.\
Цели исследования:

1. Проверка качества и целостности данных.
2. Профилирование аудитории (возраст, пол).
3. Анализ стоимости, длительности и географии поездок.
4. Формирование инсайтов для продуктовой и маркетинговой команд.

Анализ выполнен в **Jupyter Notebook** с использованием `pandas`, `numpy`, `matplotlib`, `seaborn`.

## Данные

| Поле                                                                 | Описание                       |
| -------------------------------------------------------------------- | ------------------------------ |
| `age`                                                                | возраст пользователя           |
| `gender_cd`                                                          | пол (0 — женщина, 1 — мужчина) |
| `trip_cost_rub`                                                      | стоимость поездки, ₽           |
| `distance_km`                                                        | длина маршрута, км             |
| `lvn_state_nm`                                                       | регион                         |
| `education_level_cd`, `marital_status_cd`, `loyalty_accrual_bns_amt` | дополнительные признаки        |

> **Размер**: \~900 000 строк\
> **Источник**: выгрузка стартапа kicksharing (датасет № 9 Яндекс.Практикума).

## Ключевые шаги анализа

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('data/kicksharing.csv')

df.info()
sns.heatmap(df.isna(), cbar=False)

df = df.drop(columns=['loyalty_accrual_bns_amt'])

sns.histplot(df['age'])
df['trip_cost_rub'].describe()
```

## Основные выводы

- **Возраст**: средний 31 год (диапазон 12–94).
- **Пол**: мужчин ≈ 4 × больше, чем женщин.
- **Средняя стоимость**: 128 ₽; **средний кэшбэк**: 37 ₽.
- **Дистанция**: в среднем 4 км.
- **География**: лидеры ― Москва и МО, Санкт‑Петербург.
- Аудитория концентрируется в сегменте **18–38 лет**.

## Как запустить

```bash
git clone https://github.com/<username>/kicksharing-eda.git
cd kicksharing-eda
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
jupyter notebook EDA_scooter.ipynb
```

