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
3. 🟢 [Симуляция обработки сетевых пакетов](https://github.com/AnastasiaP261/stepik_alghoritms_2#%D1%81%D0%B8%D0%BC%D1%83%D0%BB%D1%8F%D1%86%D0%B8%D1%8F-%D0%BE%D0%B1%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B8-%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D1%8B%D1%85-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2)
    <kbd>network_packet_processing.py</kbd> 
4. 🟢 [Стек с поддержкой максимума](https://github.com/AnastasiaP261/stepik_alghoritms_2#%D1%81%D1%82%D0%B5%D0%BA-%D1%81-%D0%BF%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%BA%D0%BE%D0%B9-%D0%BC%D0%B0%D0%BA%D1%81%D0%B8%D0%BC%D1%83%D0%BC%D0%B0)
    <kbd>stack_with_max.py</kbd>   
5. 🟢 [Максимум в скользящем окне](https://github.com/AnastasiaP261/stepik_alghoritms_2#%D0%BC%D0%B0%D0%BA%D1%81%D0%B8%D0%BC%D1%83%D0%BC-%D0%B2-%D1%81%D0%BA%D0%BE%D0%BB%D1%8C%D0%B7%D1%8F%D1%89%D0%B5%D0%BC-%D0%BE%D0%BA%D0%BD%D0%B5)
    <kbd>max_in_a_sliding_window.py</kbd>
6. 🟢 [Построение кучи](https://github.com/AnastasiaP261/stepik_alghoritms_2#%D0%BF%D0%BE%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BA%D1%83%D1%87%D0%B8)
    <kbd>heap_building.py</kbd>   
7. 🟢 [Параллельная обработка](https://github.com/AnastasiaP261/stepik_alghoritms_2#%D0%BF%D0%B0%D1%80%D0%B0%D0%BB%D0%BB%D0%B5%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BE%D0%B1%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B0)
    <kbd>parallel_proc.py</kbd>   
8. 🟢 [Объединение таблиц](https://github.com/AnastasiaP261/stepik_alghoritms_2#%D0%BE%D0%B1%D1%8A%D0%B5%D0%B4%D0%B8%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5-%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86)
    <kbd>sys_of_disjoint_sets.py</kbd>   
   
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

    return height


def main():
    n = int(input())
    print(calc(list(map(int, input().split()))))
```

## Симуляция обработки сетевых пакетов
Постановка задачи:
>Ваша цель — реализовать симулятор обработки сетевых пакетов. Для i-го пакета известно время его поступления 
> _arrival<sub>i</sub>_, а также время _duration<sub>i</sub>_, необходимое на его  обработку. В вашем распоряжении
> имеется один процессор, который обрабатывает пакеты в порядке их поступления. Если процессор начинает обрабатывать
> пакет _i_ (что занимает время _duration<sub>i</sub>_), он не прерывается и не останавливается до тех пор, пока не
> обработает пакет.  
> У компьютера, обрабатывающего пакеты, имеется сетевой буфер размера _size_. До начала обработки пакеты хранятся
> в буфере. Если буфер полностью заполнен в момент поступления пакета (есть _size_ пакетов, поступивших ранее, 
> которые до сих пор не обработаны), этот пакет отбрасывается и уже не будет обработан. Если несколько пакетов 
> поступает в одно и то же время, они все будут сперва сохранены в буфер (несколько последних из них могут быть 
> отброшены, если буфер заполнится). Компьютер обрабатывает пакеты в порядке их поступления. Он начинает обрабатывать
> следующий пакет из буфера сразу после того, как обработает текущий пакет. Компьютер может простаивать, если 
> все пакеты уже обработаны и в буфере нет пакетов. Пакет освобождает место в буфере сразу же, как компьютер 
> заканчивает его обработку.
> 
> **Формат входа.** Первая строка входа содержит размер буфера _size_ и число пакетов _n_. Каждая из следующих _n_ 
> строк содержит два числа: время _arrival<sub>i</sub>_ прибытия _i_-го пакета и время _duration<sub>i</sub>_, 
> необходимое на его обработку. 
> Гарантируется, что _arrival<sub>1</sub> ≤ arrival<sub>2</sub> ≤ ··· ≤ arrival<sub>n</sub>_. При этом может 
> оказаться, что _arrival<sub>i - 1</sub> = arrival<sub>i</sub>_.
> В таком случае считаем, что пакет _i − 1_ поступил раньше пакета _i_.  
> **Формат выхода.** Для каждого из _n_ пакетов выведите
> время, когда процессор начал его обрабатывать, или _−1_, если пакет был отброшен.  
> **Ограничения.** Все числа во входе целые. _1 ≤ size ≤ 10<sup>5</sup>_; _0 ≤ n ≤ 10<sup>5</sup>_;
> _0 ≤ arrivali ≤ 10<sup>6</sup>_; _0 ≤ duration<sub>i</sub> ≤ 10<sup>4</sup>_; 
> _arrival<sub>i</sub> ≤ arrival<sub>i + 1</sub>_ для всех _1 ≤ i ≤ n − 1_.

Заведем очередь фиксированного размера, которая будет эмулировать буфер. При поступлении нового пакета проверяем, 
в какой момент времени закончится обработка первого пакета в очереди. Если это число не больше, чем момент времени,
в который поступил текущий пакет(в таком случае в буфере есть свободное место), то добавляем его в 
очередь. Если больше, то пакет будет отброшен. 

Код:
``` python
from collections import deque


def processing(buf_size, packets):
    buffer = deque([], maxlen=buf_size)
    answer = []
    for i in range(buf_size):
        buffer.append(0)

    for pack in packets:
        if buffer[0] <= pack[0]:
            answer.append(max(buffer[-1], pack[0]))
            buffer.append(max(buffer[-1], pack[0]) + pack[1])
        else:
            answer.append(-1)

    return answer


def main():
    buf_size, num_p = map(int, input().split())
    if num_p == 0:
        return
    packets = [list(map(int, input().split())) for _ in range(num_p)]

    print('\n'.join(map(str, processing(buf_size, packets))))
```

## Стек с поддержкой максимума
Постановка задачи:
>В данной задаче ваша цель — расширить интерфейс стека так, чтобы он дополнительно поддерживал операцию max 
> и при этом чтобы время работы всех операций по-прежнему было константным.  
> **Формат входа.** Первая строка содержит число запросов _q_. Каждая из 
> последующих _q_ строк задаёт запрос в одном из следующих форматов: push v, pop, or max.  
> **Формат выхода.** Для каждого запроса max выведите (в отдельной строке) текущий максимум на стеке.  
> **Ограничения.** _1 ≤ q ≤ 400 000_, _0 ≤ v ≤ 100 000_.

Код:
``` python
import re
from sys import stdin, stdout


def proc_stack_command(com, stack):
    if re.match(r'push', com):
        v1 = int(com.split()[-1])
        if len(stack) == 0 or v1 > stack[-1][1]:
            v2 = v1
        else:
            v2 = stack[-1][1]
        stack.append([v1, v2])
    elif re.match(r'pop$', com):
        if stack:
            stack.pop()
    elif re.match(r'max$', com):
        if stack:
            return stack[-1][1]
        return 0


def main():
    n = int(stdin.readline())

    stack = []
    for _ in range(n):
        answ = proc_stack_command(stdin.readline(), stack)
        if type(answ) == int:
            stdout.write(str(answ) + '\n')
```

## Максимум в скользящем окне
Постановка задачи:
>Найти максимум в каждом окне размера _m_ данного массива чисел _A[1 . . . n]_.  
> **Формат входа.** Первая строка входа содержит число _n_, вторая — массив _A[1 . . . n]_, третья — число _m_.  
> **Формат выхода.** _n − m + 1_ максимумов, разделённых пробелами.   
> **Ограничения.** _1 ≤ n ≤ 10<sup>5</sup>_, _1 ≤ m ≤ n_, _0 ≤ A[i] ≤ 10<sup>5</sup>_ для всех _1 ≤ i ≤ n_.  

Используем реализацию очереди на двух стеках. 

Код:
``` python
def to_put(q, num):
    if not q or q[-1][1] <= num:
        q.append([num, num])
    else:
        q.append([num, q[-1][1]])


def to_shift(q1, q2):
    for i in range(len(q1)):
        to_put(q2, q1.pop()[0])


def search_max_in_win(win_size, nums):
    q1 = []
    q2 = []
    answer = []

    for i in range(len(nums)):
        if len(q1) < win_size:
            to_put(q1, nums[i])

        if len(q1) == win_size:
            to_shift(q1, q2)
            answer.append(q2.pop()[1])
        elif q2:
            answer.append(max(q1[-1][1], q2[-1][1]))
            q2.pop()

    return answer


def main():
    n = int(input())
    nums = list(map(int, input().split()))
    win_size = int(input())

    print(' '.join(map(str, search_max_in_win(win_size, nums))))
```

## Построение кучи

Постановка задачи:
> Переставить элементы заданного массива чисел так, чтобы он удовлетворял свойству мин-кучи.  
> **Формат входа**. Первая строка содержит число _n_. Следующая строка задаёт массив чисел _A[0], ..., A[n − 1]_.    
> **Формат выхода**. Первая строка выхода должна содержать число обменов _m_, которое должно удовлетворять неравенству 
> _0 ≤ m ≤ 4n_. Каждая из последующих _m_ строк должна задавать обмен двух элементов массива A. Каждый обмен задаётся
> парой различных индексов _0 ≤ i != j ≤ n−1_. После применения всех обменов в указанном порядке массив должен 
> превратиться в мин-кучу, то есть для всех _0 ≤ i ≤ n − 1_ должны выполняться следующие два условия:
> - если _2i + 1 ≤ n − 1_, то _A[i] < A[2i + 1]_.
> - если _2i + 2 ≤ n − 1_, то _A[i] < A[2i + 2]_. 
> 
> **Ограничения**. _1 ≤ n ≤ 105_; _0 ≤ A[i] ≤ 10<sup>9</sup>_ для всех _0 ≤ i ≤ n−1_; все A[i] попарно различны; 
> _i != j_.

Код:
``` python
from math import floor
from sys import stdin, stdout
exchanges = []


class Heap:
    def __init__(self, arr):
        self.heap = arr

    def parent(self, i):
        return floor((i - 1) / 2)

    def left_child(self, i):
        return 2 * i + 1

    def right_child(self, i):
        return 2 * i + 2

    def sift_down(self, i, stack):
        max_i = i
        l = self.left_child(i)
        if l < len(self.heap) and self.heap[l] < self.heap[max_i]:
            max_i = l
        r = self.right_child(i)
        if r < len(self.heap) and self.heap[r] < self.heap[max_i]:
            max_i = r

        if i != max_i:
            exchanges.append([i, max_i])
            self.heap[i], self.heap[max_i] = self.heap[max_i], self.heap[i]
            self.sift_down(max_i, stack)


def build_heap(n, arr):
    arr = Heap(arr)
    for i in range(n // 2 - 1, -1, -1):
        stack = []
        arr.sift_down(i, stack)


def main():
    n = int(stdin.readline())
    arr = list(map(int, stdin.readline().split()))

    build_heap(n, arr)
    stdout.write(str(len(exchanges)) + '\n')
    if exchanges:
        stdout.write('\n'.join(map(lambda x: f'{x[0]} {x[1]}', exchanges)))
```

## Параллельная обработка

Постановка задачи:
> В данной задаче ваша цель — реализовать симуляцию параллельной обработки списка задач. Такие обработчики 
> (диспетчеры) есть во всех операционных системах.  
> У вас имеется _n_ процессоров и последовательность из _m_ задач. Для каждой задачи дано время, необходимое на её 
> обработку. Очередная работа поступает к первому доступному процессору (то есть если доступных процессоров несколько,
> то доступный процессор с минимальным номером получает эту работу).  
> **Формат входа**. Первая строка входа содержит числа _n_ и _m_. Вторая содержит числа _t<sub>0</sub>, ..., 
> t<sub>m-1</sub>_, где _t<sub>i</sub>_ — время, необходимое на обработку i-й задачи. 
> Считаем, что и процессоры, и задачи нумеруются с нуля.  
> **Формат выхода**. Выход должен содержать ровно _m_ строк: i-я (считая с нуля) строка должна содержать номер 
> процессора, который получит i-ю задачу на обработку, и время, когда это произойдёт.
> **Ограничения**. _1 ≤ n ≤ 10<sup>5</sup>_; _1 ≤ m ≤ 10<sup>5</sup>_; _0 ≤ t<sub>i</sub> ≤ 10<sup>9</sup>_.


Код:
``` python
import heapq


def main():
    n, m = map(int, input().split())
    processors = []
    for i in range(n):
        heapq.heappush(processors, [0, i])

    for task_time in map(int, input().split()):
        proc = heapq.heappop(processors)
        print(f'{proc[1]} {proc[0]}')
        heapq.heappush(processors, [proc[0] + task_time, proc[1]])
```

## Объединение таблиц

Постановка задачи:
> Ваша цель в данной задаче — реализовать симуляцию объединения таблиц в базе данных. В базе данных есть _n_ таблиц, 
> пронумерованных от _1_ до _n_, над одним и тем же множеством столбцов (атрибутов). Каждая таблица содержит либо 
> реальные записи в таблице, либо символьную ссылку на другую таблицу. Изначально все таблицы содержат 
> реальные записи, и i-я таблица содержит _r<sub>i</sub>_ записей. Ваша цель — обработать _m_ запросов типа 
> (_destination<sub>i</sub>_, _source<sub>i</sub>_).  
> **Формат входа**. Первая строка содержит числа _n_ и _m_ — число таблиц и число запросов, соответственно. Вторая 
> строка содержит _n_ целых чисел _r<sub>1</sub>, ..., r<sub>n</sub>_ — размеры таблиц. Каждая из последующих _m_ строк содержит два 
> номера таблиц _destination<sub>i</sub>_ и _source<sub>i</sub>_, которые необходимо объединить.  
> **Формат выхода**. Для каждого из _m_ запросов выведите максимальный размер таблицы после соответствующего объединения.  
> **Ограничения**. _1 ≤ n_, _m ≤ 100 000_; _0 ≤ r<sub>i</sub> ≤ 10 000_; _1 ≤ destination<sub>i</sub>_, 
> _source<sub>i</sub> ≤ n_.

Код:
``` python
_max = 0


def find(i, parent):
    if i != parent[i]:
        parent[i] = find(parent[i], parent)
    return parent[i]


def union(dest, source, parent, rank):
    global _max
    d_parent = find(dest, parent)
    s_parent = find(source, parent)

    if d_parent != s_parent:
        parent[s_parent] = d_parent
        rank[d_parent] += rank[s_parent]
        _max = max(_max, rank[d_parent])
    return _max


def main():
    global _max

    n, m = map(int, input().split())    # число таблиц, число запросов
    parent = [i for i in range(n)]
    rank = list(map(int, input().split()))
    _max = max(rank)

    for _ in range(m):
        dest, source = map(int, input().split())
        print(union(dest - 1, source - 1, parent, rank))
```

## Автоматический анализ программ
Постановка задачи:
> Проверить, можно ли присвоить переменным целые значения, чтобы выполнить заданные равенства вида 
> _x<sub>i</sub> = x<sub>j</sub>_ и неравенства вида _x<sub>p</sub> != x<sub>q</sub>_.
> **Формат входа.** Первая строка содержит числа _n_, _e_, _d_. Каждая из следующих _e_ строк содержит два числа 
> _i_ и _j_ и задаёт равенство _x<sub>i</sub> = x<sub>j</sub>_. Каждая из следующих _d_ строк содержит два числа 
> _i_ и _j_ и задаёт неравенство _x<sub>i</sub> != x<sub>j</sub>_. Переменные индексируются с 1: 
> _x<sub>1</sub>, .., x<sub>n</sub>_.  
> **Формат выхода.** Выведите 1, если переменным _x<sub>1</sub>, .., x<sub>n</sub>_ можно присвоить целые значения, 
> чтобы все равенства и неравенства выполнились. В противном случае выведите 0.  
> **Ограничения.** _1 ≤ n ≤ 10<sup>5</sup>_; _0 ≤ e, d_; _e + d ≤ 2 · 10<sup>5</sup>_; _1 ≤ i, j ≤ n_.


Код:
``` python
def find(i, parent):
    if i != parent[i]:
        parent[i] = find(parent[i], parent)
    return parent[i]


def union(i, j, parent, rank):
    i_parent = find(i, parent)
    j_parent = find(j, parent)

    if i_parent == j_parent:
        return
    if rank[i_parent] > rank[j_parent]:
        parent[j_parent] = i_parent
    else:
        parent[i_parent] = j_parent
        if rank[i_parent] == rank[j_parent]:
            rank[j_parent] += 1


def main():
    n, e, d = map(int, input().split())  # число переменных, кол-во равенств, кол-во неравенств
    parents = [i for i in range(n)]
    rank = [1 for _ in range(n)]

    code = 1
    if e != 0:
        for i in range(e):
            n1, n2 = map(int, input().split())
            union(n1 - 1, n2 - 1, parents, rank)

    if d != 0:
        for i in range(d):
            n1, n2 = map(int, input().split())
            if find(n1 - 1, parents) == find(n2 - 1, parents):
                code = 0

    print(code)
```


## Телефонная книга
Постановка задачи:
> Цель в данной задаче — реализовать простую телефонную книгу, поддерживающую три следующих типа запросов. 
> С указанными ограничениями данная задача может быть решена с использованием таблицы с прямой адресацией.
> - `add number name`: добавить запись с именем _name_ и телефонным номером _number_. Если запись с таким телефонным
    > номером уже есть, нужно заменить в ней имя на _name_. 
> - `del number`: удалить запись с соответствующим телефонным номером. Если такой записи нет, ничего не делать.
> - `find number`: найти имя записи с телефонным номером _number_. Если запись с таким номером есть, вывести имя. 
    > В противном случае вывести _«not found»_ (без кавычек).  
> 
> **Формат входа.** Первая строка содержит число запросов _n_. Каждая из следующих _n_ строк задаёт запрос в одном из 
> трёх описанных выше форматов.  
> **Формат выхода.** Для каждого запроса find выведите в отдельной строке либо имя, либо «not found».  
> **Ограничения.** _1 ≤ n ≤ 10<sup>5</sup>_. Телефонные номера содержат не более семи цифр и не содержат ведущих 
> нулей. Имена содержат только буквы латинского алфавита, не являются пустыми строками и имеют длину не больше 15.
> Гарантируется, что среди имён не встречается строка «not found».


Код:
``` python
phone_book = dict()


def add_in_book(entry):
    phone_num, name = entry.split()
    phone_book[phone_num] = name


def del_from_book(phone_num):
    phone_book.pop(phone_num, '')


def main():
    n = int(input())
    for i in range(n):
        request, entry = input().split(maxsplit=1)
        if request == 'add':
            add_in_book(entry)
        elif request == 'del':
            del_from_book(entry)
        elif request == 'find':
            print(phone_book.get(entry, 'not found'))
```


## Хеширование цепочками
Постановка задачи:
>

Текст

Код:
``` python

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