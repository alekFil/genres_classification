# Классификация жарнов на основе обложки музыкального альбома

## А. Подготовка данных

Изучены данные: 10 классов альбомов, общее количество изображений - 7800.
Обнаружены особенности: дисбаланс классов, максимальное количество изображений в классе 'country' (1485), минимальное в 'rap' (327).
Обработаны данные: удалены 52 дубликата.
Разработаны функции для загрузки данных и разделения выборки.

## Б. Моделирование

Построена бейзлайн модель: использован метод ближайших соседей на основе библиотеки FAISS с эмбеддингами ResNet50.
Оценено качество:
  Бейзлайн модель: weighed F1 = 0.49.
  Модели классического ML: SVC - 0.62, RandomForestClassifier - 0.45, CatBoostClassifier - 0.61.
  Нейросеть с применением простой аугментации изображений: weighed F1 = 0.6269.

В рамках проведения экспериментов проведена простая аугментация изображений (0.6319), случайная аугментация изображений (0.6208), применение кастомной аугментации изображений (GridMask, 0.6213), устранение дисбаланса классов методом кастомного оверсемплинга (0,6257).

## В. Оценка качества модели

Проведена оценка лучшей на тестовой выборке: weighed F1 = 0.601.

Анализ матрицы ошибок показал:
Хорошее различение классов anime и black_metal. Проблемы с классификацией disco (71% ошибок), часто путается с country (19%), pop (15%), и даже anime (10%). При этом, следует отметить, что обложки альбомов diso, edm, pop и rap нередко сложно отличись даже человеку.

## Дальнейшая работа

С учетом проведенной работы полагается целесообразным осуществить следующую доработку:
1. Расширить данные дополнительными экземплярами классов, устанив дисбаланс классов и увеличив выборки (с использованием MusizBrainz API и Spotify API).
2. Провести кластеризацию изображений с целью выявления трудноразличимых классов, попытаться дополнительными преобразованиями увеличить "расстояние" между ними.
3. Выделить из изображений дополнительные признаки, например:
    - наличие лица на изображении;
    - наличие человека на изображении;
    - наличие группы людей на изображении;
    - стиль изображения (мультипликация, фото и др.);
    - оценку структуры изображения;
    - оценку цвета изображения;
    - оценку текстуры изображения.
4. Применит новые признаки в комбинации с изображением: встроить в нейросеть или использовать эмбеддинги. Возможно с понижением размерности.
5. Разработать интрефейс взаимодействия клиентов и модели (раширить класс для полной проверки на валидность и отображения характеристик автомобилей).
6. Реализовать веб-приложение, демонстрирующее работу модели. Например, с использованием streamlit.
