# Тестовое задание

Приложение для управления контактами:

- **Добавлять контакты**: создавать новые записи с именем, телефоном и email.
- **Редактировать контакты**: вносить изменения в существующие контакты.
- **Удалять контакты**: удалять ненужные контакты из списка.
- **Искать контакты**: использовать поисковую строку для быстрого поиска по имени.

Данные сохраняются в localStorage, что обеспечивает их доступность при перезагрузке страницы.

## Структура компонентов

1. **Контактный список** (`ContactList.vue`): отображает список контактов.
2. **Поисковая строка** (`SearchBar.vue`): позволяет искать контакты по имени.
3. **Форма для добавления и редактирования контактов** (`ContactForm.vue`): форма для ввода/редактирования данных.
4. **Модальное окно** (`BaseModal.vue`): используется для отображения формы добавления/редактирования контактов.
5. **Кнопки и базовые компоненты**: для работы с интерфейсом.

## Настройка проекта

```sh
npm install
```

### Режим разработки

```sh
npm run dev
```

### Сборка для продакшена

```sh
npm run build
```
- [ссылка на Демо](https://to.karaudio.ru/)
