# Library-os
Вызов `import os`

## Методы
### --------
`os.getcwd()` — узнать текущую рабочую директорию

Input:
```python
import os

current_directory = os.getcwd()
print(f"Сейчас мой скрипт работает отсюда: {current_directory}")
```
Output:
```python
Сейчас мой скрипт работает отсюда: C:\Users\Alex\Documents\Project 1
```

### --------
`os.chdir()` — сменить текущую директорию

Input:
```python
import os

print(f"Сначала я здесь: {os.getcwd()}")

# 'Переходим' в папку data (она должна быть внутри текущей директории)
os.chdir('data')

print(f"Теперь я здесь: {os.getcwd()}")
```
А как вернуться обратно, на уровень выше? Для этого используется стандартное обозначение:
```python
import os

os.chdir('..')
print(f"И снова я здесь: {os.getcwd()}")
```
### Важный момент: если вы попытаетесь перейти в папку, которой не существует, Python выдаст ошибку FileNotFoundError, и скрипт упадет. 

### --------

Запуск на исполнение

С этой задачей прекрасно справляется метод startfile, которому стоит передать адрес необходимо объекта. Программное обеспечение, используемое для открытия документа, определяется средой автоматически
```python
import os
os.startfile(r"D:\test.txt")
```

## Работа с папками

### --------

`os.listdir()` — посмотреть, что находится в папке

Если вызвать без аргументов, покажет содержимое текущей папки

Input:
```python
import os

whats_inside = os.listdir()
print(f"Внутри этой папки лежат: {whats_inside}")
```
Output:
```python
Внутри этой папки лежат:
['main.py', '.venv', 'data', 'requirements.txt']
```
Можно заглянуть и в любую другую папку, просто передав ей путь в качестве аргумента: 
```python
os.listdir('C:/Users/ИмяПользователя/Documents')
```
### --------

`os.mkdir()` — создает одну папку

Тут всё просто. mkdir (make directory) создает новую папку в текущей директории.
```python
import os

# Создаст папку 'reports' прямо здесь
os.mkdir('reports')
```
Важный нюанс: если папка reports уже существует, скрипт упадет с ошибкой FileExistsError.

### --------

`os.makedirs()` — создать сразу несколько папок
А что, если нужно создать целую структуру? Например, `archive/2025/photos`. Если попытаться сделать это через `mkdir`, он сломается, потому что папки `archiv`e еще нет. Вот тут-то и нужен `makedirs` — он достаточно умен, чтобы создать всё дерево директорий за вас.
```python
import os

# Эта команда создаст и 'archive', и вложенную в нее '2025', и 'photos'
os.makedirs('archive/2025/photos')
```
### --------

`os.rmdir()` — удалить пустую папку

`rmdir` (remove directory) делает обратное — удаляет папку. Ключевое слово здесь — пустую. Если внутри директории что-то есть, Python откажется ее удалять и выдаст ошибку.
```python
import os

# Сначала создадим, потом удалим
os.mkdir('temp_folder')
os.rmdir('temp_folder')
```
## Работа с файлами

### --------

`os.rename()` — переименовать или переместить файл

Команда `rename` делает сразу две вещи.
```python
import os

# Сначала создадим файл, чтобы было с чем работать
with open('old_name.txt', 'w') as f:
    f.write('some text')

# А теперь переименуем его
os.rename('old_name.txt', 'new_name.txt')
```
Перемещение файла: Если вторым аргументом указать путь в другую папку, файл переедет туда.
```python
import os
os.makedirs('archive') # Создадим папку для примера

# Перемещаем наш файл в папку 'archive'
os.rename('new_name.txt', 'archive/new_name.txt')
```
### --------

`os.remove()` — удалить файл
```python
import os

# Удаляем файл, который только что переместили
os.remove('archive/new_name.txt')
```
## ВНИМАНИЕ! ОЧЕНЬ ВАЖНЫЙ БЛОК!
Команды `os.remove()` и `os.rmdir()` удаляют файлы и папки НАВСЕГДА. Они не перемещают их в Корзину. Отменить это действие нельзя. Один неверный шаг в цикле — и можно случайно снести половину рабочего стола.

Золотое правило: прежде чем запускать скрипт, который что-то удаляет, сначала замените `os.remove(path)` на `print(f"Собираюсь удалить: {path}")`. Запустите, посмотрите на список и только потом, будучи на 100% уверенным, возвращайте команду удаления. Не рискуйте.

### --------

 магия `os.path` - путь к файлу

На Windows пути к файлам разделяются обратным слэшем: `C:\Users\User\Documents`.
А на Linux и macOS — прямым: `/home/user/documents`.

`os.path.join()` - Эта функция сама понимает, на какой операционной системе она запущена, и подставляет правильный разделитель.

```python
import os

# Просто перечисляем части пути через запятую
folder = 'documents'
filename = 'report.docx'

# os.path.join() сделает всю грязную работу за нас
full_path = os.path.join('C:', 'Users', 'User', folder, filename)

print(full_path)
# На Windows выведет: C:\Users\User\documents\report.docx
# На Linux вывело бы: C:/Users/User/documents/report.docx (с правильными слэшами)
```
### --------

`basename` и `dirname` — разбираем пути на запчасти
```python
os.path.basename(path) — возвращает имя файла.

os.path.dirname(path) — возвращает путь к директории.
```
```python
import os

full_path = '/home/user/documents/report.docx'

filename = os.path.basename(full_path)
print(f"Имя файла: {filename}") # Выведет: Имя файла: report.docx

directory = os.path.dirname(full_path)
print(f"Путь к папке: {directory}") # Выведет: Путь к папке: /home/user/documents
```
### --------

Проверки — работаем безопасно
Это, возможно, самый важный блок в этой главе. Помните, мы говорили, что скрипт упадет, если попытаться перейти в несуществующую папку? Или создать папку, которая уже есть? Чтобы этого избежать, нужно проверять, существует ли путь, прежде чем что-то с ним делать.

`os.path.exists(path)` — самая частая проверка. Возвращает True, если путь (файл или папка) существует, и False, если нет.

`os.path.isfile(path)` — возвращает True, только если это существующий файл.

`os.path.isdir(path)` — возвращает True, только если это существующая папка.

```python
import os

path_to_check = 'archive'

if os.path.exists(path_to_check):
    print(f"Путь '{path_to_check}' существует.")
    if os.path.isdir(path_to_check):
        print("И это папка!")
    elif os.path.isfile(path_to_check):
        print("И это файл!")
else:
    print(f"Пути '{path_to_check}' не существует. Давайте создадим папку.")
    os.makedirs(path_to_check)
```
### --------

### Вычисление размера

`getsize()` - Вычесление размера документа или папки

Input:
```python
import os
print(os.path.getsize("D:\\test.txt"))
```
Output:
```python
136226 # размер в байтах
```
