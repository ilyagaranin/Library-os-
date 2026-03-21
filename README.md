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
### №3
`os.chdir()` — сменить текущую директорию

Input:
```python
print(f"Сначала я здесь: {os.getcwd()}")

# 'Переходим' в папку data (она должна быть внутри текущей директории)
os.chdir('data')

print(f"Теперь я здесь: {os.getcwd()}")
```
А как вернуться обратно, на уровень выше? Для этого используется стандартное обозначение:
```python
os.chdir('..')
print(f"И снова я здесь: {os.getcwd()}")
```
### Важный момент: если вы попытаетесь перейти в папку, которой не существует, Python выдаст ошибку FileNotFoundError, и скрипт упадет. 
## Работа с папками
### №4

`os.mkdir()` — создает одну папку
