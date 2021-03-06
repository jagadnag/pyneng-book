.. raw:: latex

   \newpage

Задания
=======

.. include:: ./pytest.rst

Задание 11.1
~~~~~~~~~~~~

Создать функцию parse_cdp_neighbors, которая обрабатывает вывод команды show cdp neighbors.

У функции должен быть один параметр command_output, который ожидает как аргумент вывод команды одной строкой (не имя файла). Для этого надо считать все содержимое файла в строку,
а затем передать строку как аргумент функции (как передать вывод команды показано в коде ниже).

Функция должна возвращать словарь, который описывает соединения между устройствами.

Например, если как аргумент был передан такой вывод:

::

    R4>show cdp neighbors

    Device ID    Local Intrfce   Holdtme     Capability       Platform    Port ID
    R5           Fa 0/1          122           R S I           2811       Fa 0/1
    R6           Fa 0/2          143           R S I           2811       Fa 0/0

Функция должна вернуть такой словарь:

.. code:: python

    {("R4", "Fa0/1"): ("R5", "Fa0/1"),
     ("R4", "Fa0/2"): ("R6", "Fa0/0")}

В словаре интерфейсы должны быть записаны без пробела между типом и именем. То есть так Fa0/0, а не так Fa 0/0.

Проверить работу функции на содержимом файла sh_cdp_n_sw1.txt. При этом функция работать
и на других файлах (тест проверяет работу функции на выводе из sh_cdp_n_sw1.txt и sh_cdp_n_r3.txt).

dd
Ограничение: Все задания надо выполнять используя только пройденные темы.

.. code:: python

    def parse_cdp_neighbors(command_output):
        """
        Тут мы передаем вывод команды одной строкой потому что именно в таком виде
        будет получен вывод команды с оборудования. Принимая как аргумент вывод
        команды, вместо имени файла, мы делаем функцию более универсальной: она может
        работать и с файлами и с выводом с оборудования.
        Плюс учимся работать с таким выводом.
        """


    if __name__ == "__main__":
        with open("sh_cdp_n_sw1.txt") as f:
            print(parse_cdp_neighbors(f.read()))


Задание 11.2
~~~~~~~~~~~~

Создать функцию create_network_map, которая обрабатывает
вывод команды show cdp neighbors из нескольких файлов и объединяет его в одну общую топологию.

У функции должен быть один параметр filenames, который ожидает как аргумент список с именами файлов, в которых находится вывод команды show cdp neighbors.

Функция должна возвращать словарь, который описывает соединения между устройствами.
Структура словаря такая же, как в задании 11.1:

.. code:: python

    {("R4", "Fa0/1"): ("R5", "Fa0/1"),
     ("R4", "Fa0/2"): ("R6", "Fa0/0")}


Cгенерировать топологию, которая соответствует выводу из файлов:

* sh_cdp_n_sw1.txt
* sh_cdp_n_r1.txt
* sh_cdp_n_r2.txt
* sh_cdp_n_r3.txt

В словаре, который возвращает функция create_network_map, не должно быть дублей.

С помощью функции draw_topology из файла draw_network_graph.py нарисовать схему на основании топологии, полученной с помощью функции create_network_map.
Результат должен выглядеть так же, как схема в файле task_11_2_topology.svg

.. figure:: https://raw.githubusercontent.com/natenka/pyneng-examples-exercises/master/exercises/11_modules/task_11_2_topology.png

При этом:

* Расположение устройств на схеме может быть другим
* Соединения должны соответствовать схеме

Не копировать код функций parse_cdp_neighbors и draw_topology.

Ограничение: Все задания надо выполнять используя только пройденные темы.

.. note::
    Для выполнения этого задания, должен быть установлен graphviz:
    ``apt-get install graphviz``

    И модуль python для работы с graphviz:
    ``pip install graphviz``


.. code:: python

    # эти заготовки написаны чтобы показать в какой момент должна
    # рисоваться топология (после вызова функции)
    def create_network_map(filenames):
        pass


    if __name__ == "__main__":
        infiles = [
            "sh_cdp_n_sw1.txt",
            "sh_cdp_n_r1.txt",
            "sh_cdp_n_r2.txt",
            "sh_cdp_n_r3.txt",
        ]

        topology = create_network_map(infiles)
        # рисуем топологию:
        # draw_topology(topology)

