# Ex.08 Design of Interactive Image Gallery
developed by SUDHARSAN.s
24009664
# Date:25/11/2024
# AIM:
To design a web application for an inteactive image gallery with minimum five images.

# DESIGN STEPS:
## Step 1:
Clone the github repository and create Django admin interface.

## Step 2:
Change settings.py file to allow request from all hosts.

## Step 3:
Use CSS for positioning and styling.

## Step 4:
Write JavaScript program for implementing interactivity.

## Step 5:
Validate the HTML and CSS code.

## Step 6:
Publish the website in the given URL.

# PROGRAM :
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Photo Gallery</title>
    <style>
        /* Basic styling */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            text-align: center; /* Center the content */
        }
        h1 {
            font-size: 2.5em; /* Bigger font size */
            color: #fff;
            background: linear-gradient(135deg, #FF6F61, #FFB6C1);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.5);
            margin-top: 20px;
            font-weight: bold;
            letter-spacing: 1px;
        }
        h1 span {
            display: block;
            font-size: 1.5em; /* Smaller font size for the second line */
            margin-top: 5px;
        }
        .gallery {
            display: flex;
            flex-direction: row;
            justify-content: center; /* Center the gallery */
            align-items: center;
            gap: 15px;
            overflow-x: auto;
            padding: 20px;
            white-space: nowrap;
        }
        .gallery-item {
            display: inline-block;
            cursor: pointer;
        }
        .gallery-item img {
            height: 200px; /* Consistent height */
            border-radius: 10px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .gallery-item img:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        .modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80%;
            max-width: 800px;
            background: white;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            border-radius: 10px;
            padding: 20px;
            z-index: 1000;
        }
        .modal img {
            width: 100%;
            border-radius: 10px;
        }
        .modal h2 {
            margin-top: 15px;
            text-align: center;
        }
        .modal p {
            margin-top: 10px;
            text-align: center;
        }
        .close-modal {
            display: block;
            margin: 20px auto 0;
            padding: 10px 20px;
            background: #333;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .close-modal:hover {
            background: #555;
        }
        .overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 999;
        }
    </style>
</head>
<body>
    <h1>
        SUDHARSAN S<br>
        <span>24009664</span><br>
        Interactive Image Gallery
    </h1>
    <div class="gallery">
        <!-- Gallery Items -->
        <div class="gallery-item" data-title="One Piece" data-description="Set sail on a boundless sea of dreams, where friendship is the ultimate treasure, courage defies the odds, and the pursuit of freedom turns an ordinary crew into legends" data-image="C:\Users\sudharshan\OneDrive\Desktop\environment\one piece.jpg">
            <img src="C:\Users\sudharshan\OneDrive\Desktop\environment\one piece.jpg" alt="One Piece">
        </div>
        <div class="gallery-item" data-title="Naruto" data-description="In a world of pain and darkness, the will to never give up illuminates a path where bonds become unbreakable, dreams transform into destiny, and even the smallest spark can ignite a blazing fire." data-image="C:\Users\sudharshan\OneDrive\Desktop\environment\naruto.jpg">
            <img src="C:\Users\sudharshan\OneDrive\Desktop\environment\naruto.jpg" alt="Naruto">
        </div>
        <div class="gallery-item" data-title="Solo Leveling" data-description="From the depths of powerlessness rises a lone hunter, defying limits, shattering chains, and standing as the ultimate force in a world where strength defines survival" data-image="C:\Users\sudharshan\OneDrive\Desktop\environment\solo leveling.jpg">
            <img src="C:\Users\sudharshan\OneDrive\Desktop\environment\solo leveling.jpg" alt="Solo Leveling">
        </div>
        <div class="gallery-item" data-title="Jujutsu Kaisen" data-description="In a battle where curses lurk in the unseen, a heart of steel and the weight of loss forge a sorcerer, balancing life, death, and the will to protect what truly matters." data-image="C:\Users\sudharshan\OneDrive\Desktop\environment\jjk.jpg">
            <img src="C:\Users\sudharshan\OneDrive\Desktop\environment\jjk.jpg" alt="Jujutsu Kaisen">
        </div>
        <div class="gallery-item" data-title="Bleach" data-description="When the line between life and death blurs, a blade guided by resolve protects the fragile bonds of humanity, carving a path through the shadowy dance of souls." data-image="C:\Users\sudharshan\OneDrive\Desktop\environment\bleach.jpg">
            <img src="C:\Users\sudharshan\OneDrive\Desktop\environment\bleach.jpg" alt="Bleach">
        </div>
        <div class="gallery-item" data-title="Dan Da Dan" data-description="In a whirlwind of bizarre encounters and otherworldly chaos, unlikely allies discover that amidst the weirdness, courage and connection are the ultimate superpowers" data-image="C:\Users\sudharshan\OneDrive\Pictures\Screenshots\Screenshot 2024-12-15 091833.png">
            <img src="C:\Users\sudharshan\OneDrive\Pictures\Screenshots\Screenshot 2024-12-15 091833.png" alt="Dan Da Dan">
        </div>
    </div>

    <!-- Modal and Overlay -->
    <div class="overlay"></div>
    <div class="modal">
        <h2 id="modal-title"></h2>
        <img id="modal-image" src="" alt="Modal Image">
        <p id="modal-description"></p>
        <button class="close-modal">Close</button>
    </div>

    <script>
        // JavaScript for Modal and Interactivity
        document.addEventListener('DOMContentLoaded', () => {
            const galleryItems = document.querySelectorAll('.gallery-item');
            const modal = document.querySelector('.modal');
            const overlay = document.querySelector('.overlay');
            const modalTitle = document.getElementById('modal-title');
            const modalImage = document.getElementById('modal-image');
            const modalDescription = document.getElementById('modal-description');
            const closeModalButton = document.querySelector('.close-modal');

            galleryItems.forEach(item => {
                item.addEventListener('click', () => {
                    const title = item.getAttribute('data-title');
                    const description = item.getAttribute('data-description');
                    const image = item.getAttribute('data-image');

                    modalTitle.textContent = title;
                    modalDescription.textContent = description;
                    modalImage.src = image;

                    modal.style.display = 'block';
                    overlay.style.display = 'block';
                });
            });

            closeModalButton.addEventListener('click', () => {
                modal.style.display = 'none';
                overlay.style.display = 'none';
            });

            overlay.addEventListener('click', () => {
                modal.style.display = 'none';
                overlay.style.display = 'none';
            });
        });
    </script>
</body>
</html>

views.py
 from django.shortcuts import render
def gallery(request):
    return render(request,"galery.html")

def index(request):
    result = None  # To store the calculation result
    if request.method == 'POST':
        try:
            # Retrieve inputs from the POST request
            voltage = float(request.POST.get('voltage'))
            resistance = float(request.POST.get('resistance'))
            
            # Validate resistance to avoid division by zero
            if resistance > 0:
                result = (voltage ** 2) / resistance
                
                # Log inputs and outputs to the server console
                print(f"Input received - Voltage: {voltage}V, Resistance: {resistance}Ω")
                print(f"Calculated Power: {result}W")
            else:
                result = "Resistance must be greater than zero."
                print("Error: Resistance must be greater than zero.")
        except ValueError:
            result = "Invalid input. Please enter numeric values."
            print("Error: Invalid input. Non-numeric values entered.")
    else:
        print("GET request received; no calculation performed.")
    
    return render(request, 'index.html', {'result': result})
 urls.py
"""
URL configuration for lamp_power project.

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/5.1/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import path
from myapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
   # path('glry/',views.gallery),
    #path('', views.index, name='index'),
    path('gallery/',views.gallery)
]
```



# OUTPUT:
![Screenshot 2024-12-15 115938](https://github.com/user-attachments/assets/611348db-6569-4765-a27c-12b41ae0d214)
![Screenshot 2024-12-15 115859](https://github.com/user-attachments/assets/881eb3de-cac9-4ac7-8723-3036e9fe74b2)


# RESULT:
The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
