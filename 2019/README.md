# Темы для дипломов и курсовых

## Базы данных
- Есть работающая библиотека https://github.com/tshemsedinov/node-mysql-utilities
  можно ее развивать:
  - Поддржка промисов и async/await
  - Оптимизация, поддержка
  - Поддержка драйвера [mysql2](https://github.com/sidorares/node-mysql2)
- Разработка аналогов `node-mysql-utilities` для:
  - PostgreSQL: https://github.com/tshemsedinov/node-pgsql-utilities
  - Oracle: https://github.com/tshemsedinov/node-oracle-utilities
- Построители запросов (query builders) для: MongoDB, IndexedDB, SQLite и др.
- Разработка прототипа СУБД
  - Варианты модели даннх: реляционная, ключ-значение, колоночная, объектная,
  документная, графовая
  - Хранение: файловая система, оперативная память, другая СУБД
  - Доступ к данным: файловая система, сетевой протокол, IPC, API (встраиваемая)

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

## Работа со схемами
- Генерация SQL скриптов из схем
- Генерация структуры коллекций Mongodb и GlobalStorage индексов из схем

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

## Metasync
Репозиторий https://github.com/metarhia/metasync
- Примитивы параллельного программирования
