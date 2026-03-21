# Library-os
Вызов `import os`

## Команды
### №1
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
### №2
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
Можно заглянуть и в любую другую папку, просто передав ей путь в качестве аргумента: 
```python
os.listdir('C:/Users/ИмяПользователя/Documents')
```

`os.chdir()` — сменить текущую директорию
