# Course_work_ML
Сoursework on machine learning by students Rogozinskaya Anna and Smirnov Ilya
Система управления роботом-манипулятором – это решение на основе методов глубокого обучения и компьютерного зрения, в основе которой лежит фреймворк PyTorch версии 1.9 для создания и обучения нейронных сетей, работающий совместно с OpenCV 4.5 для обработки визуальных данных в реальном времени. Архитектура нейронной сети объединяет возможности CNN и LSTM сетей. Сверточная часть реализована на базе ResNet-50, выступающего в роли основного энкодера изображений. После предварительного обучения на общих данных, сеть была адаптирована специально под задачи управления роботом. LSTM модуль содержит три последовательных слоя по 256 нейронов, обрабатывающих временные последовательности и предсказывающих динамику системы.
Система компьютерного зрения включает несколько ключевых компонентов, т.к. для сегментации объектов используется архитектура U-Net, реализованная с помощью Segmentation Models PyTorch, а определение положения объектов в пространстве осуществляется через PoseNet, обученную на комбинации реальных и синтетических данных. Трекинг объектов реализован на основе DeepSORT алгоритма. Обработка данных выполняется с использованием библиотек NumPy и SciPy, обеспечивающих эффективные численные вычисления. Предобработка включает стандартизацию входных данных, расширение обучающей выборки через аугментацию с помощью Albumentations и фильтрацию шумов на основе фильтра Калмана из библиотеки filterpy.
Управляющая система реализована как многоуровневый контроллер, верхний уровень представлен вариационным автоэнкодером для генерации траекторий движения, имеющим архитектуру энкодера [input_dim, 512, 256, latent_dim] с симметричным декодером, нижний уровень реализует непосредственное управление через нейросетевой контроллер.
ля обучения системы используется оптимизатор Adam с начальной скоростью обучения 3e-4 и постепенным уменьшением по косинусному расписанию. Регуляризация осуществляется через dropout с вероятностью 0.3 и L2-регуляризацию с коэффициентом 1e-4. Обучение проводится на минибатчах размером 64 с использованием комбинированной функции потерь, включающей среднеквадратичную ошибку для реконструкции, KL-дивергенцию для вариационного автоэнкодера и временную разность для обучения с подкреплением.
Взаимодействие компонентов системы организовано на основе асинхронного подхода с использованием asyncio, для обмена данными между модулями применяется система очередей из библиотеки queue, а синхронизация различных потоков данных реализована через threading, визуализация процесса обучения и мониторинг метрик осуществляются с помощью matplotlib и seaborn.
PyViz для создания интерактивных визуализаций процесса обучения и работы робота, логирование выполняется через стандартную библиотеку logging с настроенным форматированием и ротацией логов. Для отслеживания экспериментов и сохранения моделей используется простая система на основе JSON-файлов. Применяются методы векторизации вычислений через NumPy, многопоточная обработка данных с помощью ThreadPoolExecutor и эффективное управление памятью. Управление зависимостями осуществляется через requirements.txt с фиксированными версиями библиотек для обеспечения воспроизводимости результатов. 
