# ShopEase Cloud 2.0 - Prototype
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Secretos - ShopEase Cloud 2.0</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
        <a class="navbar-brand" href="{{ url_for('index') }}">Secretos</a>
        
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ms-auto">
                <li class="nav-item">
                    <a class="nav-link" href="{{ url_for('index') }}">Home</a>
                </li>

                <li class="nav-item">
                    <a class="nav-link" href="{{ url_for('cart') }}">Cart</a>
                </li>

                {% if session.get('username') %}
                    <li class="nav-item">
                        <a class="nav-link" href="{{ url_for('logout') }}">Logout</a>
                    </li>

                    {% if session.get('username') == 'admin' %}
                        <li class="nav-item">
                            <a class="nav-link" href="{{ url_for('dashboard') }}">Dashboard</a>
                        </li>
                    {% endif %}
                {% else %}
                    <li class="nav-item">
                        <a class="nav-link" href="{{ url_for('login') }}">Login</a>
                    </li>
                {% endif %}
            </ul>
        </div>
    </div>
</nav>

<!-- Page Content -->
<div class="container mt-4">
    {% block content %}
    {% endblock %}
</div>

<!-- Footer -->
<footer class="bg-light text-center text-muted py-3 mt-5">
    Secretos — ShopEase Cloud 2.0 Prototype
</footer>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

</body>
</html


## Features

- **Home page** – product listings
- **Login/Logout** – session-based authentication
- **Search** – filter products by name
- **Product detail** – with simulated AI recommendations
- **Shopping cart** – add items and simulate checkout/payment
- **Admin dashboard** – analytics stats (admin login only)

## Running Locally

```bash
pip install -r requirements.txt
python app.py
```

Then open http://localhost:5000

**Demo credentials:**
- `admin` / `password123` (has dashboard access)
- `user1` / `pass1`

## Deploying to Azure Web App

1. Push this repo to GitHub.
2. In Azure Portal, create a **Web App** (Python 3.11, Linux).
3. Under **Deployment Center**, connect your GitHub repo.
4. Set the **Startup Command** to:
   ```
   gunicorn --bind=0.0.0.0 --timeout 600 app:app
   ```
5. Azure will auto-deploy on every push to your main branch.

## Project Structure

```
app.py              # Main Flask application
requirements.txt    # Python dependencies
startup.txt         # Azure startup command reference
templates/
    base.html       # Shared layout
    index.html      # Home / product listing
    login.html      # Login form
    search.html     # Search results
    product.html    # Product detail + AI recommendations
    cart.html       # Shopping cart + checkout
    dashboard.html  # Admin analytics dashboard
```
