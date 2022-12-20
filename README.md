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
Ссылка на моего телеграмм бота [https://t.me/vvot19_polik_bot]

