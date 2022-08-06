# Документацию по stdio.h в SynapseOs
Итак,ты наверное пробовал использовать <stdio.h> для SynapseOs? Я думаю да, раз ты читаешь это. В данном гайде я хочу показать, как работать с этим вашим input/output. Если вы ищете определённую функцию, советую Ctrl-F
Ну, поехали!
> - Так, ну и где ваши stdio.h вообще находятся?
> - Они разбросаны по всей структуре OS! И в kernel/src, kernel/include и ещё где либо.
Как же это работает? Насколько я понял в kernel описываються методы, а сами методы лежать от apps до Владивостока. Допустим основной код stdio.h находиться в libc(apps/libc), а описание его функций в keneral/include/libk/stdio.h
Тем не менее, сейчас я покажу какие функции есть в stdio!
И да кстати, эта документация будет расширяться по мере добавления новый функций и (моих припадков желания работать)
## Часть первая, printf и print, rand и srand
### void printf(char *text, ...)
Самый часто используемый print, который выдаёт нормальный вывод(это тот же print но, без создания вручную va_list и тп и тд)
Что бы понять как с ним работать прочитайте таблицу из информации о методе print и используйте таким образом:

`printf("%формат", "ТипоТип, который нужен для формата")`
### void print(char *format, va_list args)
Данный print является часто используемым, но только в своей обёртке, в printf
Так как для каждого типа есть свой принт, данная функция выбирает тип с помощью передаваемого ему аргумент format.
А args нужен для передачи данный для принта(int, char, hex, и тому подобное)
#### Вот таблица форматов, которые можно передавать в format:
- %s - для вывода стандартной строки
- %c - для вывода одного char из строки или просто одного char
- %d - наверное сделали на будущие, что бы выводить тип double, но пока что, выводит стандартный int
- %i - для вывода обычного int
- %u - для вывода unsigned int(Обычный int, но с натуральными и не натуральными числами)
- %x - для вывода типа хекса(hex), требует аргумент с типом uint32_t
### void putint(const int i)
Простой вывод int
### int print_str(char str[])
Основа для всех методов вывода, выводит строку!
И зачем-то всегда возвращает 0?
### void putchar(unsigned char ch)
Выводит одну char.
Обёртка над printf
### uint64_t rand()
Да, стандартная функция рандома, везде одинаково...
Используйте srand, что бы сделать рандом более реалистичным 
И кстати, если вы не использовали rand в программирование обычных приложений, гугл в помощь, ищите как это работает!
### uint64_t srand(uint32_t seed)
Я не знаю, зачем 0Nera решил, что srand должен что-то возращать, но это его дело, не моё) 
srand используют для изменения сида для повышения реалистичности рандома(часто в нём используют как seed системное время)




PS - Если мой довольно кривой пуллреквест примут, я ещё допишу в документацию о работе с файлами