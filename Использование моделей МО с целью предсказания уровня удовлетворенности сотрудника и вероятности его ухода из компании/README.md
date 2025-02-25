# Предсказание уровня удовлетворённости и вероятности увольнения сотрудников

## Цели проекта
1. Построить модель для предсказания **уровня удовлетворённости сотрудников** компании.
2. Построить модель для предсказания **вероятности увольнения сотрудников**.

---

## Описание данных
- **id** — уникальный идентификатор сотрудника.
- **dept** — отдел, в котором работает сотрудник.
- **level** — уровень занимаемой должности.
- **workload** — уровень загруженности сотрудника.
- **employment_years** — длительность работы в компании (в годах).
- **last_year_promo** — было ли повышение за последний год.
- **last_year_violations** — нарушения трудового договора за последний год.
- **supervisor_evaluation** — оценка качества работы сотрудника.
- **salary** — ежемесячная зарплата.
- **job_satisfaction_rate** — уровень удовлетворённости сотрудника (целевой признак для первой задачи).

---

## Этапы работы

### Задача 1: Предсказание уровня удовлетворённости сотрудников
#### 1. Загрузка и предобработка данных
- Данные соответствуют описанию задачи, названия и типы столбцов корректны.
- Пропуски в данных обработаны с помощью пайплайна.
- Дубликаты отсутствуют.

#### 2. Исследовательский анализ данных
- Данные в тренировочной и тестовой выборках распределены схожим образом.
- Дисбаланс признаков (например, большинство сотрудников имеют уровень junior) отражает реальную ситуацию.
- Выбросы (видны на boxplot) соответствуют реальным значениям.

#### 3. Подготовка данных и обучение моделей
- Признаки подготовлены с помощью пайплайна.
- Обучены четыре модели:
  1. **DecisionTreeRegressor**
  2. **LinearRegression**
  3. **KNeighborsRegressor**
  4. **SVR**

- Лучшие результаты:
  - Модель: **DecisionTreeRegressor** с параметрами:
    - `max_depth=17`
    - `max_features=7`
    - `random_state=42`
  - **Метрика SMAPE** на тестовой выборке: **16.53**.

---

### Задача 2: Предсказание увольнения сотрудников
#### 1. Загрузка и предобработка данных
- Данные соответствуют описанию задачи, названия и типы столбцов корректны.
- Пропуски обработаны, дубликаты отсутствуют.

#### 2. Исследовательский анализ данных
- Данные из тренировочной и тестовой выборок распределены схожим образом.
- Дисбаланс признаков отражает реальную ситуацию (например, большинство сотрудников junior).
- Добавлен новый признак **job_satisfaction_rate**, предсказанный моделью из первой задачи.

#### 3. Портрет «уволившегося сотрудника»
- **Отдел**: technology.
- **Уровень загруженности**: low.
- **Средняя зарплата**: 23,885 рублей (меньше, чем у оставшихся — 37,702 рублей).
- **Уровень удовлетворённости**:
  - Чем выше удовлетворённость, тем меньше вероятность увольнения.

#### 4. Обучение моделей
- Признаки подготовлены с помощью пайплайна.
- Обучены четыре модели:
  1. **DecisionTreeClassifier**
  2. **LogisticRegression**
  3. **KNeighborsClassifier**
  4. **SVC**

- Лучшие результаты:
  - Модель: **DecisionTreeClassifier** с параметрами:
    - `max_depth=5`
    - `max_features=9`
    - `random_state=42`
  - **Метрика AUC** на тестовой выборке: **0.9188**.

---

## Выводы и рекомендации
1. **Уровень удовлетворённости сотрудников**:
   - Модель DecisionTreeRegressor показала SMAPE = **16.53**.
   - Можно использовать модель для прогнозирования удовлетворённости сотрудников, однако требуется дополнительная работа для улучшения точности.

2. **Предсказание увольнения сотрудников**:
   - Модель DecisionTreeClassifier показала AUC = **0.9188**.
   - Уровень удовлетворённости влияет на вероятность увольнения: сотрудники с низким уровнем удовлетворённости чаще уходят.

3. **Рекомендации**:
   - Повысить уровень удовлетворённости сотрудников (например, за счёт увеличения зарплаты).
   - Автоматизировать процессы для сотрудников с низкой загруженностью, чтобы снизить издержки.
   - Использовать разработанные модели для прогнозирования оттока сотрудников и принятия превентивных мер.
