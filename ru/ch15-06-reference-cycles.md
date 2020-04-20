## Ссылочные зацикливания могут приводить к утечке памяти

Гарантии безопасности памяти в Rust затрудняют, но не делают невозможным случайное выделения памяти, которая никогда не очищается (что известно как *утечка памяти* ). Полное предотвращение утечек памяти не гарантируется Rust, так же как не является гарантией отсутствие гонок данных проверенных во время компиляции, а это означает, что утечки памяти безопасны в Rust. Мы можем увидеть, что Rust допускает утечки памяти, используя типы `Rc<T>` и `RefCell<T>`: можно создавать связи, где элементы ссылаются друг на друга в цикле. Это приводит к утечкам памяти, поскольку счётчик ссылок каждого элемента в цикле никогда не достигнет 0, а значения никогда не будут удалены.

<img alt="Reference cycle of lists" src="../../rustbook-en/src/img/trpl15-04.svg" class="center">

![test image](https://i.imgur.com/k2y3saw.png)