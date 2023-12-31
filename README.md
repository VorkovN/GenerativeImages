**Автор:** Ворков Никита    
**Задача:** Сегментация     
**Датасет** Cityscapes      
**Архитектура:** Unet       

**Инструкция к запуску:**
1. Из файла "requirements.txt" подтянуть нужные библиотеки
2. Скачать с сайта "cityscapes-dataset.com" архив с исходными изображениями "leftImg8bit" и распаковать его в папке datasets
3. Распаковать один из двух архивов "gtFine_color.tar.xz" или "gtFine_mono.tar.xz" и переименовать его в "gtFine". В датасете gtFine_color лежат изображения закодированные в формате rgb, а в датасете gtFine_mono лежат изображение закодированное в gray scale
4. Для запуска обучения нужно запустить один из двух ноутбуков "Unet_training_color.ipynb" или "Unet_training_mono.ipynb" в зависимости от того, какой датасет был выбран

P.S. Мой размеченный датасет отличается от оригинального размеченного датасета тем, что вместо 33 размеченных классов, как в оригинальном датасете в моем датасете размечено всего 7 классов. Сделано это с целью ускорения обучения до адекватной метрики в рамках лабораторной работы. 
Представленные классы получились путем обобщения сущностей из первоначальных классах. Так из разные типы транспорта превратились просто в класс транспорта. Разные типы дороги превратились просто в дорогу и тп. Пкерерисовка изображений осуществлялась с помощью скрипта "images_color_changer.ipynb"

**Результаты экспериментов:**
* Результаты экспериментов на тестовой выборке можно посмотреть в автодополняемом файле "results.txt" в папке "results".
* Результаты(loss по каждой итерации и dice score по каждой эпохе) выводимые на tensorboard можно посмотреть в папке "run"
* Получившиеся изображения можно посмотреть в папке "results"

**Выводы**
1. Оптимайзер Adam и SGD справляются почти одинаково хорошо
2. Оптимайзер SGD требует  learning rate в 100 раз больше, чем Adam
3. Повышение моментума для SGD с 0.9 до 0.95 несколько улучшило метрики
4. Обучение выходит на плато примерно за 20 эпох
5. Обучение на цветных масках занимал больше времени, чем на монотонных в 1,5 раза (1.7it/s vs 1.1 it/s)