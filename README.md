### NAME: SURYA P <br>
### REG NO: 212224230280 <br> 
### Date: 28/08/2025

## EX. No. 5 : SERVER SIDE PROCESSING

## AIM :
 To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side. 


## FORMULA :
P = I<sup>2</sup>R
<br> P --> Power (in watts)
<br> I --> Intensity
<br> R --> Resistance

## DESIGN STEPS :

### Step 1
Clone the repository from GitHub.

### Step 2
Create Django Admin project.

### Step 3
Create a New App under the Django Admin project.

### Step 4
Create python programs for views and urls to perform server side processing.

### Step 5
Create a HTML file to implement form based input and output.

### Step 6
Publish the website in the given URL.

## PROGRAM :

### Power.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Electric Power Calculator | P = I²R</title>
<style>
  :root {
    --card-bg: #ffffff;
    --page-bg-from: #fff4e6;
    --page-bg-to: #ffe6f0;
    --header: #40312f;
    --accent: #ffb366;
    --accent-2: #ffd699;
    --muted: #666;
    --shadow-md: 0 8px 30px rgba(0,0,0,0.12);
    --border-radius: 12px;
  }

  body {
    margin: 0;
    padding: 18px;
    font-family: "Segoe UI", Roboto, Arial, sans-serif;
    background: linear-gradient(135deg, var(--page-bg-from), var(--page-bg-to));
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
  }

  .container {
    width: 100%;
    max-width: 450px;
    background: var(--card-bg);
    border-radius: var(--border-radius);
    box-shadow: var(--shadow-md);
    padding: 20px 30px;
  }

  h1 {
    text-align: center;
    font-size: 22px;
    color: var(--header);
    margin: 0 0 20px 0;
    text-decoration: underline;
  }

  .form-group {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
    font-size: 14px;
    font-weight: 600;
    color: var(--header);
  }

  .form-group label {
    flex-basis: 45%;
    text-align: right;
    padding-right: 10px;
  }

  .form-control {
    flex-basis: 55%;
    display: flex;
    align-items: center;
  }

  input[type="text"] {
    padding: 8px;
    border-radius: 6px;
    border: 1px solid rgba(0,0,0,0.2);
    flex-grow: 1;
    min-width: 0;
    color: var(--header);
  }

  .unit {
    width: 40px;
    font-size: 0.9em;
    padding-left: 5px;
  }

  input[type="submit"] {
    background-color: var(--accent);
    color: var(--header);
    padding: 10px 15px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 1em;
    font-weight: 600;
    transition: background-color 0.3s ease;
    width: 100%;
    margin-top: 10px;
  }

  input[type="submit"]:hover {
    background-color: var(--accent-2);
  }

  .result-group {
    background: var(--accent-2);
    padding: 10px;
    border-radius: 6px;
    margin-top: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  @media (max-width: 500px){
    .form-group label { font-size: 13px; }
    input[type="text"] { font-size: 13px; padding:6px; }
    input[type="submit"] { font-size: 14px; }
  }
</style>
</head>
<body>

<div class="container">
  <h1>Electric Power Calculator</h1>

  <form method="POST">
    {% csrf_token %}

    <div class="form-group">
      <label for="id_intensity">Current (I):</label>
      <div class="form-control">
        <input type="text" id="id_intensity" name="Intensity" placeholder="e.g., 5" value="{{ i }}" required>
        <span class="unit">A</span>
      </div>
    </div>

    <div class="form-group">
      <label for="id_resistance">Resistance (R):</label>
      <div class="form-control">
        <input type="text" id="id_resistance" name="Resistence" placeholder="e.g., 10" value="{{ r }}" required>
        <span class="unit">Ω</span>
      </div>
    </div>

    <input type="submit" value="Calculate Power (P = I²R)">

    {% if Power %}
    <div class="result-group">
      <label for="id_power">Power (P):</label>
      <div class="form-control">
        <input type="text" id="id_power" readonly value="{{ Power }}">
        <span class="unit">W</span>
      </div>
    </div>
    {% endif %}
  </form>
</div>

</body>
</html>

```

### Urls.py :
```python
from django.contrib import admin
from django.urls import path
from powercalc import views  # <-- this is fine if __init__.py exists

urlpatterns = [
    path('admin/', admin.site.urls),
    path('Power/', views.power, name="Power"),
    path('', views.power, name="Power"),  # default page
]

```

### Views.py :
```python
from django.shortcuts import render

def power(request):
    context = {'Power': '', 'i': '', 'r': ''}
    if request.method == 'POST':
        I = request.POST.get('Intensity', '')
        R = request.POST.get('Resistence', '')
        if I.replace('.', '', 1).isdigit() and R.replace('.', '', 1).isdigit():
            Power = float(I) ** 2 * float(R)
            context['Power'] = Power
        context['i'] = I
        context['r'] = R
    return render(request, 'power.html', context)

```
## SERVER SIDE PROCESSING :
<img width="1472" height="477" alt="image" src="https://github.com/user-attachments/assets/1fa847f0-3eb0-47ca-a6a2-5b0e6f3b2429" />

## HOMEPAGE:
<img width="789" height="486" alt="image" src="https://github.com/user-attachments/assets/dca56d17-45fe-4bb7-abc6-e757333e7104" />

## RESULT:
The program for performing server side processing is completed successfully.
