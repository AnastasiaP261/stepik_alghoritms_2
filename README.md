# Задачи с курса Stepik "Алгоритмы: Теория и практика. Структуры данных"
[Cсылка на курс](https://stepik.org/course/1547/info)

В этом репозитории я буду продолжать собирать решения задач со второй части курса по алгоритмам.


###  Статусы задач:
- 🟢 - задача решена и прошла все внутренние тесты платформы
- 🟡 - задача решена, но не все тесты платформы пройдены

### Другие обозначения:
- <kbd>file_name</kbd> - имя файла решения данной задачи

###  Содержание:
1. 🟢 [Расстановка скобок в коде](https://github.com/AnastasiaP261/stepik_alghoritms_2#%D1%80%D0%B0%D1%81%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-%D1%81%D0%BA%D0%BE%D0%B1%D0%BE%D0%BA-%D0%B2-%D0%BA%D0%BE%D0%B4%D0%B5)
    <kbd>brace_placement.py</kbd>
2. 🟢 [Высота дерева](https://github.com/AnastasiaP261/stepik_alghoritms_2#%D0%B2%D1%8B%D1%81%D0%BE%D1%82%D0%B0-%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%B0)
    <kbd>tree_height.py</kbd>   
   
## Расстановка скобок в коде
Постановка задачи:
>**Формат входа.** Строка _s[1..n]_, состоящая из заглавных и прописных букв латинского алфавита,
> цифр, знаков препинания и скобок из множества []{}().  
> **Формат выхода.** Если скобки в _s_ расставлены правильно, выведите
строку "Success". В противном случае выведите индекс (используя индексацию с единицы) 
> первой закрывающей скобки, для которой нет соответствующей открывающей. Если такой нет, 
> выведите индекс первой открывающей скобки, для которой нет соответствующей закрывающей.

Используем стэк для решения задачи.

Код:
``` python
from collections import deque


def counting_braces(s):
    stack = deque([])
    braces = {'(': ')', '[': ']', '{': '}'}

    for i, ch in enumerate(s, 1):
        if ch in braces.keys():
            stack.append((ch, i))
        elif ch in braces.values():
            if not stack:
                return i
            elif ch == braces[stack[-1][0]]:
                stack.pop()
            else:
                return i

    if not stack:
        return 0
    return stack[-1][1]


def main():
    s = input()

    answer = counting_braces(s)
    if answer == 0:
        print('Success')
    else:
        print(answer)
```

## Высота дерева
Постановка задачи:
> **Формат входа.** Первая строка содержит натуральное число _1 ≤ n ≤ 10<sup>5</sup>_. Вторая строка содержит _n_ целых 
> чисел _parent<sub>0</sub>, ..., parent<sub>n−1</sub>_. Для каждого _0 ≤ i ≤ n−1_, _parenti_ — родитель вершины _i_; 
> если _parenti_ = _−1_, то _i_ является корнем. Гарантируется, что корень ровно один. Гарантируется, что данная 
> последовательность задаёт дерево.  
> **Формат выхода.** Высота дерева.

Сначала преобразуем входной массив (который является списком родителей) в список детей (или список смежностей).
Создадим очередь, в которую добавим вершину-корень и ограничитель уровня(благодаря ему мы сможем отслеживать, когда
мы перешли на более низкий уровень дерева). Далее в цикле проходя по очереди извлекаем из нее каждую вершину и 
добавляем ее детей. Если встречаем ограничитель, то увеличиваем счетчик высоты на 1.
Сложность данного алгоритма выйдет О(n).

Код:
``` python
def transformation(parents_list, n):
    adj_list = [[] for _ in range(n)]
    root_index = -1

    for child, parent in enumerate(parents_list, 1):
        if parent != -1:
            adj_list[parent].append(child - 1)
        else:
            root_index = child - 1

    return adj_list, root_index


def calc(_list):
    _list, root = transformation(_list, len(_list))
    height = 1
    queue = []

    queue.extend(_list[root])
    if len(queue) == 0:
        return height
    else:
        queue.append(-1)            # ограничитель уровня

    while queue:
        cur_peak = queue.pop(0)
        if cur_peak == -1:
            height += 1
            if queue: queue.append(-1)
        else:
            queue.extend(_list[cur_peak])

    print(height)
    return height


def main():
    n = int(input())
    print(calc(list(map(int, input().split()))))
```

<!---
## Название
Постановка задачи:
>

Текст

Код:
``` python

```
-->