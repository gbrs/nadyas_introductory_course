## PANDAS

import pandas as pd

### Названия колонок и индексы
df.columns - "список" названий колонок  
df.index - "список" индексов (названий строк)

### Работа с файлами
df = pd.read_csv('path_to_your.csv', encoding='Windows-1251', sep=';') - чтение файла в датафрейм  
df.to_csv('myDataFrame.csv', index=False) - запись датафрейма в файл  
s = pd.Series([3, -5, np.nan, 4]) - создание серии

### Создание и удаление столбиков
df['total'] = df.math + df.phys + df.bio - создаем новый столбец суммы оценок  
df.drop(["Team", "Weight"], axis = 1) - удалить два столбца в копии дф  
df.drop_duplicates() - удалить дубликаты в копии

### Обращение к элементам
s[1:3] - срез из серии  
df['A'] или df.A - серия из колонки A  
df[0:10] - дф из 10 строк  
df[["Age", "Sex"]] - дф из двух колонок  
df.iloc[0] - серия из строки 0  
df.iloc[2, 7] - данные из ячейки (2-я строка, 7-ой столбец)  
df.iloc[0:5, 0:3] - дф из первых 5 строчек и 3 столбцов  
df.loc[0:4, 'shape':'shape'] - дф из одного столбика  
df.sample(50) - выдаст рандомный набор данных из 50 строк

### Инфо
df.info() - общая информация о дф: по колоночно тип данных, кол-во ненулевых значений  
df.shape - размерность датафрейма  
df.dtypes - имеющиеся типы данных  
df.nunique() - количество уникальных значений в каждой колонке  
df.column_name.unique() - возвращает массив из уникальных элементов колонки  
df.column_name.value_counts() - количество для каждого уникального значения в серии

### Агрегационные функции
df.sum(axis=1), min(), count(), mean(), round(), idxmin(), cumsum(), prod()

### Фильтрация
s[(s > 0.3) & (s < 0.8)]  
df[df['math score']>60]  
df.loc[(df['B'] < 25) & (df['C'] >= -40), 'A']  
df.query("gender == 'female' & math_score >= 85")

### Группировка
df.groupby('sex').sum()  
df.groupby('sex', dropna=False).agg(['mean', 'median'])

### Джойны
pd.merge(left_df, right_df, on='key') - слияние по одноименным столбцам key  
pd.merge(df1, df2, left_index=True, right_on='name') - слияние по индексу и столбцу

### Пропуски
df.isnull().mean() - выдаст долю пропусков  
df[df.col_name.isnull()] - выдаст строки, где в колонке есть NA  
df.isna().sum() - узнаем количество NaNов в каждом столбце   
df.notnull() - противоположность метода isnull()  
df.notna().sum() - узнаем количество неNaNов в каждом столбце  
df.fillna(value=5) - заполняем все NaNы пятерками (возвращается копия)  
df.dropna()   создает «копию», удалив все строки (по умолчанию) со значением NaN  

### Статистика
df.describe() - описательные статистики по всем числовым данным  
df.describe(include='all') - описательные статистики по всем данным  
df.mean() - среднее по столбикам  
median, mode, var, std, quantile(0.05)  
df.corr() - выдаст таблицу коэффициентов корреляции числовых столбиков  

### Разное
df.pivot_table([values = ]"Salary", [index = ]"Executor", [columns = ]"Type") - сводная таблица  
df.sort_values('Country') - сортировка по значению  
pd.to_datetime([datetime(2015, 7, 3), '4th of July, 2015', '2015-Jul-6', '07-07-2015', '20150708']) - самые разные по формату объекты умеет превращать в дату  
df.col_name.str.lower() - применение методов строк ко всем значениям колонки  
df.groupby('payment_type').total.agg('sum').plot.pie() - построение диаграммы



## SEABORN

import seaborn as sns

### Загрузка датасетов
df = sns.load_dataset('iris') - загрузить датасет  
sns.get_dataset_names()

### Распределения
sns.histplot(data=df, x='Gender', hue='Gender', hue_order=['M', 'F']) - гистограмма  
sns.kdeplot(data=df, x='Purchase', hue='Gender') - ~ плотность вероятности  
sns.ecdfplot(data=penguins, x="bill_length_mm", hue="species") - функция распределения  
sns.violinplot(x="species", y="sepal_length", hue="gender", data=iris,  
                       split=True, inner="quartile",  
                       palette=["lightblue", "lightpink"]);

### "Столбики"
sns.barplot(data=df, x="island", y="body_mass_g", hue="sex")  
  sns.countplot(data=df, x="class", hue="alive")  
sns.boxplot(data=df, x="class", y="age", hue="alive")  

### Линии
sns.lineplot(data=flights, x="year", y="passengers", hue="month")  
sns.scatterplot(data=tips, x="total_bill", y="tip", hue="size")  
  sns.regplot(x=x_data, y=y_data, order=2)  
  sns.lmplot(x='math_score', y='reading_score', hue='gender', data=df) - скаттерплот: точки – ученики, по умолчанию линия линейной регрессии, легенда

### Разное
sns.heatmap(glue, annot=True)



## SCIPY

import scipy.stats as sps

sps.norm.rvs(loc=10, scale=3, size=10000) - генерация выборки размера  N, возвращает numpy.array

Распределения:   
непрерывные - norm, uniform (равномерное), expon, t;  
дискретные - bernoulli, binom, geom, poisson, randint (равномерное).


