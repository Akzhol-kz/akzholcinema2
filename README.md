akzholcinema2/
</head>
<body>
    <h1>Добро пожаловать в Akzhol Cinema</h1>
            <a href="{{ url_for('movie', movie_id=movie.id) }}">{{ Миссия Красный }}</a>
            <img src="https://avatars.mds.yandex.net/i?id=29cf8da80b4ccd1a2f7de0926e75a212b3728bc4-5234706-images-thumbs&n=13">

        </li>
        {% endfor %}
    </ul>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ movie.title }}</title>
</head>
<body>
    <h1>{{ movie.title }}</h1>
    <p>{{ movie.description }}</p>
    <p>Цена за билет: {{ movie.price }} KZT</p>
    <form action="{{ url_for('checkout') }}" method="post">
        <input type="hidden" name="movie_id" value="{{ movie.id }}">
        <label for="tickets">Количество билетов:</label>
        <input type="number" name="tickets" id="tickets" min="1" required>
        <button type="submit">Купить</button>
    </form>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Подтверждение заказа</title>
</head>
<body>
    <h1>Спасибо за покупку!</h1>
    <p>Вы приобрели {{ tickets }} билет(а/ов) на "{{ movie.title }}".</p>
    <p>Общая стоимость: {{ total_price }} KZT</p>
    <a href="{{ url_for('index') }}">Вернуться на главную</a>
</body>
</html>
flask
body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
}
pip install flask
python app.py
