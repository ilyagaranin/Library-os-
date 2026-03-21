# Library-os
Вызов `import os`

## Команды

`os.getcwd()` — узнать текущую рабочую директорию

Input:
```python
current_directory = os.getcwd()
print(f"Сейчас мой скрипт работает отсюда: {current_directory}")
```

Output:
```python
Сейчас мой скрипт работает отсюда: C:\Users\Alex\Documents\Project 1
```

`os.listdir()` — посмотреть, что находится в папке

Если вызвать без аргументов, покажет содержимое текущей папки
Input:
```python
whats_inside = os.listdir()
print(f"Внутри этой папки лежат: {whats_inside}")
```
Output:
```python
Внутри этой папки лежат:
['main.py', '.venv', 'data', 'requirements.txt']
```
