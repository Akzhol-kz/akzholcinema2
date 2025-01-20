akzholcinema2/
├── app.py
├── requirements.txt
├── templates/
│   ├── index.html
│   ├── movie.html
│   ├── checkout.html
└── static/
    ├── styles.css
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

# Пример фильмов
movies = [
    {"id": 1, "title": "Фильм 1", "description": "Описание фильма 1", "price": 1000},
    {"id": 2, "title": "Фильм 2", "description": "Описание фильма 2", "price": 1200},
    {"id": 3, "title": "Фильм 3", "description": "Описание фильма 3", "price": 1500},
]

@app.route("/")
def index():
    return render_template("index.html", movies=movies)

@app.route("/movie/<int:movie_id>")
def movie(movie_id):
    movie = next((m for m in movies if m["id"] == movie_id), None)
    if not movie:
        return "Фильм не найден", 404
    return render_template("movie.html", movie=movie)

@app.route("/checkout", methods=["POST"])
def checkout():
    movie_id = request.form.get("movie_id")
    tickets = int(request.form.get("tickets"))
    movie = next((m for m in movies if m["id"] == int(movie_id)), None)
    if not movie:
        return "Ошибка при обработке заказа", 404
    total_price = movie["price"] * tickets
    return render_template("checkout.html", movie=movie, tickets=tickets, total_price=total_price)

if __name__ == "__main__":
    app.run(debug=True)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Akzhol Cinema</title>
</head>
<body>
    <h1>Добро пожаловать в Akzhol Cinema</h1>
    <ul>
        {% for movie in movies %}
        <li>
            <a href="{{ url_for('movie', movie_id=movie.id) }}">{{ movie.title }}</a>
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
