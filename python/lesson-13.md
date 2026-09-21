# Python · Урок 13. Обработка исключений

## Цели урока
- Перехватывать ошибки с помощью `try/except`
- Выбрасывать собственные исключения

## Теория
Исключение — ошибка во время выполнения. Если её не перехватить, программа аварийно завершится.

```python
try:
    n = int(input("Число: "))
    print(10 / n)
except ValueError:
    print("Это не число")
except ZeroDivisionError:
    print("Деление на ноль")
else:
    print("Ошибок не было")
finally:
    print("Выполняется всегда")
```

**Несколько исключений сразу**
```python
except (ValueError, TypeError) as e:
    print("Ошибка:", e)
```

**Выброс исключения**
```python
def set_age(age):
    if age < 0:
        raise ValueError("Возраст не может быть отрицательным")
    return age
```

**Собственное исключение**
```python
class InsufficientFunds(Exception):
    pass

def withdraw(balance, amount):
    if amount > balance:
        raise InsufficientFunds("Недостаточно средств")
    return balance - amount
```

**Ввод с повтором**
```python
while True:
    try:
        n = int(input("Число: "))
        break
    except ValueError:
        print("Попробуйте ещё раз")
```

## Типичные ошибки
- Голый `except:` скрывает все ошибки, включая баги — указывайте тип
- Слишком большой блок `try`
- Перехват ошибки без реакции на неё (`except: pass`)

## Практика
1. Калькулятор, не падающий при вводе букв и делении на 0.
2. Чтение файла с обработкой `FileNotFoundError`.
3. Своё исключение `InvalidEmail` для проверки адреса.

## Проверь себя
1. Когда выполняется блок `else`, а когда `finally`?
2. Чем `raise` отличается от `except`?
3. Почему плохо писать `except:` без типа?

---
[← Урок 12](lesson-12.md) · [Программа курса](README.md) · [Урок 14 →](lesson-14.md)
