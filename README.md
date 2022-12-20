### Мокеева Полина 11-902
# cloudlab-task2
---
## Система работает следующим образом:

+ Происходит заливка фотографии в bucket с именем  photos,
из-за чего тригеррится функция (ее код - **vvot19-face-detection.py**)

+ Функция делает запрос к **yandex vision** и отдает массив с координатами лица и создает message в message queue.  
Дальше если в message queue есть запись, триггерится контейнер (**Dockerfile + index.py**)

+ Контейнер достает фотографию через **boto3**, затем обрезает ее через **Pillow**,
делает запись в базе данных, где **id = message_id**, имя фотографии с лицом = **message_id+photo_name**  
И фотография лица сохраняется в новый бакет faces.

+ Затем APIGATEWAY на два разных запроса дает картинки из bucket. Функуция с вебхуком для телеграмм бота (vvot19-boot.py)  
Обработка 3 комманд /getface   /find <name>   reply_to_message_with_new_name_for_face с описанным в тз функционалом
  
---
Загрузка фотографии c лицом (/getface)
![image](https://user-images.githubusercontent.com/55764228/208752786-f4bcd2d4-3010-4701-89d1-a9f873c371b3.png)
Поиск фото (/find <name>) 
![image](https://user-images.githubusercontent.com/55764228/208752913-f4bbe40c-21e9-4268-9f3d-e7690622d4a0.png)

Ссылка на моего телеграмм бота [https://t.me/vvot19_polik_bot]

