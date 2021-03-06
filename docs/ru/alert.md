# Уведомления
----------

Уведомления - это простой способ уведомить пользователя о состоянии вашего приложения. Например, они могут информировать пользователя о завершении длительного процесса или приходе нового сообщения. В этом разделе мы покажем вам, как заставить их работать в вашем приложении.

## Одноразовые сообщения:

Flash-уведомление — это одноразовое сообщение, которое будет удалено при следующем обращении. 
Уведомления призваны информировать о непосредственно произошедшим событием, например сообщение о сохранении данных.

ORCHID имеет удобный вызов и отображение уведомлений поверх одноразовых flash-данных.


```php
use Orchid\Support\Facades\Alert;

public function store()
{
    Alert::message('Welcome Aboard!');
    return Redirect::home();
}
```

Вы также можете сделать:

```php
Alert::info('Message')
Alert::success('Message')
Alert::error('Message')
Alert::warning('Message')
```

или использовать более короткую запись:

```php
alert('Message');
```


При использовании, будет установлено несколько ключей в сессии:
- 'flash_notification.message' - Сообщение для отображения
- 'flash_notification.level' - Строка, представляющая тип уведомления

Для отображения в необходимом месте требуется:
```html
<div class="container">
    @include('platform::partials.alert')
    <p>Welcome to my website...</p>
</div>
```

## Уведомления в панели администрирования

Уведомление в панели администрирование отличается от flash-сообщений, тем, что не удаляются после просмотра и
могут быть добавлены любым пользователям даже когда они находятся не в сети. Это ещё один отличный способ информирования,
например для  приложение "менеджера задач" уведомлять сотрудника о новой задаче.

Для создания уведомления требуется:
```php
$user = User::find(1);

$user->notify(new \Orchid\Platform\Notifications\DashboardNotification([
    'title' => 'Hello Word',
    'message' => 'New post!',
    'action' => 'https://google.com',
    'type' => DashboardNotification::INFO,
]));
```

Поддерживаемые типы:

- DashboardNotification::INFO (По умолчанию)
- DashboardNotification::SUCCESS
- DashboardNotification::WARNING
- DashboardNotification::ERROR
