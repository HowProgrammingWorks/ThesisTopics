# Темы для дипломов и курсовых

Все задания, из приведенных тут, могут быть изменены, предлагайте, в каком
направлении вам интересно развить ту или иную тему. Можно брать свои темы,
но они должны содержать интересные технические решения, элементы исследований,
экспериментов с изменениями, оптимизации, реализацию алгоритмов и структур
данных, новые синтаксические конструкции.

## Транзакционные объекты
Репозиторий https://github.com/HowProgrammingWorks/Transaction
- Несколько объектов в транзакции `DatasetTransaction`
- Исправить удаление свойств `Transaction` (через значения Symbol в дельте) и
добавление/удаление объектов из `DatasetTransaction`
- Специяльный EventEmitter `.before/after/on('name', callback)`
- Журнал коммитов (храним даты, хеши)
- Блокировка объектов (повторно над объектом не стартуем)
- Каскадное реактивное изменение курсоров
- События `.on('commit')`, `.on('start')`...
- Таймауты транзакций и долгие транзакции
`Transaction.start(obj).timeout(5000);`
- Отделить прокси от транзакции
```js
const [transaction, obj2] = Transaction.start(obj);
obj2.userName = 'a';
transaction.commit();
```

## StorageProviders для GlobalStrorage
Репозиторий https://github.com/metarhia/globalstorage
- Memory - основной провайдер хранения в оперативке
- Fs - провайдер хранения в файловой системе (временного хранения, у нас in-memory СУБД)
- Mongodb - провайдер хранения в Mongodb
- Pg - провайдер хранения в PostgreSQL

## Объекты с вычисляемыми полями
- Описание полей
```js
const obj = {
  name: 'Marcus',
  city: 'Roma',
  country: 'Pax Romana'
};
const schema = {
  address() {
    return this.countru + ', ' + this.city;
  }
};
const obj2 = Calc.apply(obj, schema);
console.log(obj2.address); // 'Pax Romana, Roma'
```
- Вычисление полей
- Оборачивание в Proxy или виртуальный класс с get

## Индексы для структур данных
- Индексы для курсоров и для хранилищ в GlobalStorage
- Алгоритмы хеширования с сохранением сравнения
- Индексы по нескольким полям
- Оптимизация запросов через индексы

## Materialized Cursor
Курсоры, которые ни кем не запрошены (ни клиентским приложением, ни
бизнс-логикой) но поддерживаемые системой (вместе с индексами) потому,
что к такой агрегации данных часто обращаются.

## Работа со схемами
Репозиторий https://github.com/metarhia/metaschema
- Генерация SQL скриптов из схем
- Генерация структуры коллекций Mongodb и GlobalStorage индексов из схем
- Миграции на базе репозитория схем

## Реализация методов курсоров
- Скоро будут опубликованы сигнатуры методов API

## Инструмент для проведения семинаров с Live Coding
Репозиторий https://github.com/HowProgrammingWorks/LiveCoding
- Кеширование всех исходников на сервере
- Вычисление, пересылка и применение дельты (изменений)
- Защита от DDOS (система из очередей для балансировки)
- Подсветка синтаксиса
- Сервер (интеграция всех серверных модулей)
- Клиент (интеграция всех клиентских модулей)

## Карта репозиториев How.Programming.Works
Репозиторий https://github.com/HowProgrammingWorks/KnowledgeMap
- Построение графа зависимостей
- Поиск циклов
- Построение последовательности лекций по темам

## Менеджер пакетов
Репозиторий https://github.com/metarhia/namespace

## Реализации интерфейса fs (файловой системы)
- Для кеширования в памяти
  - Задаем определенный объем памяти для кеша
  - Собираем статистику и автоматически определяем, что лучше закешировать
- Имитация файловой системы в памяти
  - Возможность загружать в память с диска
  - Возможность сбрасывать на диск из памяти
- Для сохранения в облачных файловых хранилищах
  - Dropbox
  - Google Drive
- Песочница https://github.com/metarhia/sandboxed-fs
  - Дорабатываем по [issues](https://github.com/metarhia/sandboxed-fs/issues)

## Фреймворк для тестирования
Репозиторий https://github.com/metarhia/maojian

## Metasync
Репозиторий https://github.com/metarhia/metasync
- Простые асинхронные абстракции
  - Data collector
  - Queue

## Do
Репозиторий https://github.com/metarhia/do

## Logger
Репозиторий https://github.com/metarhia/metalog
- Задание: https://github.com/metarhia/metalog/issues/17

## Шаблоны
Репозиторий https://github.com/metarhia/tickplate

## Sandboxing

## Рефактор Readable/WritableStream в Node.js
Для буферизации записи в файл вместо односвязного списка и перекладывания из
него в массив можно выбрать только одну структуру данных, или писать сразу в
заранее преаллокированный большой буффер, а не склеивать массив буферов.