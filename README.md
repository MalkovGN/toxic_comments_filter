# Классификация токсичных комментариев

## Описание
Этот проект посвящён **классификации токсичных комментариев** с помощью модели DistilBERT. На текущем этапе модель различает только два класса (бинарная метка): **токсичный** (1) или **нетоксичный** (0).

## Что есть в проекте

1. **Загрузка и предобработка данных**  
   -  Используется датасет [из Jigsaw Toxic Comment Classification Challenge](https://www.kaggle.com/competitions/jigsaw-toxic-comment-classification-challenge/data) с текстом комментариев и шестью признаками токсичности. с текстом комментариев и шестью признаками токсичности.
   - Создаётся **бинарная метка** `label`: 1, если комментарий токсичный (хотя бы одна из шести меток = 1), иначе 0.

2. **Анализ данных**  
   - Построение графиков распределения меток (токсичные/нетоксичные).
   - Распределение длины комментариев.
   - Облако слов для нетоксичных комментариев.

3. **Модель DistilBERT**  
   - **Binary Classification**: Используется `DistilBertForSequenceClassification` с `num_labels=2`.
   - Анализируются `первые 128` токенов из комментариев, т.к. увеличение сильно нагружает память и квадратично увеличивает время обучение.


## Возможные улучшения

1. **Многометочная классификация**  
   - Вместо бинарной метки обучать модель различать **каждую** метку (`toxic`, `severe_toxic`, `obscene`, `threat`, `insult`, `identity_hate`).

2. **Weighted Loss** для дисбаланса  
   - Если токсичных комментариев значительно меньше, чем нетоксичных, добавление `pos_weight` в функцию потерь улучшит результаты для редких примеров.

3. **Oversampling / Undersampling**  
   - При сильном перекосе (мало токсичных) можно увеличить их количество (oversampling) или уменьшить нетоксичные (undersampling).

4. **Увеличение `max_length`**  
   - Если в средних или концах комментариев есть важная часть, можно увеличить `max_length`.

5. **Перевод на другие языки**  
   - Для токсичных комментариев можно попробовать парафразирование (с переводом на другой язык и обратно), чтобы увеличить разнообразие примеров.
