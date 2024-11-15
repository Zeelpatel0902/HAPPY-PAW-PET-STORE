# Happy Paw Pet Store

## Overview
Happy Paw Pet Store is an e-commerce platform tailored for pet lovers. It allows customers to shop for pet products, book appointments with veterinarians, and connect with shelters. The project also includes an admin panel for managing customers, orders, products, and more.

This project is built using **Django**, leveraging its robust features to provide a seamless user and admin experience.

## Features

### Admin Panel
- Manage customers, orders, products, and categories.
- Monitor and approve shelter homes and doctors.
- Handle feedback and gallery images.
- View and manage customer appointments.

### Customer Features
- Browse and search for pet-related products by categories and subcategories.
- Add products to the cart or wishlist.
- Place and track orders.
- Book appointments with veterinarians.
- Provide feedback and rate products.

### Database Entities
- Comprehensive models for customers, products, orders, appointments, feedback, shelters, and more.

---

## Project Structure

### **Admin Directory (`happypawpetstore_Admin`)**

#### Key Files:
1. **`app.py`**  
   - Configures the admin app for Django.
   ```python
   class happypawpetstoreAdminConfig(AppConfig):
       default_auto_field = 'django.db.models.BigAutoField'
       name = 'happypawpetstore_Admin'
   ```

2. **`forms.py`**  
   - Contains form definitions for handling admin inputs, including customer, product, order, category, and other entities.

3. **`functions.py`**  
   - Utility functions like file uploads for managing static assets (e.g., images).
   ```python
   def handle_upload_file(f):
       with open('happypawpetstore_Admin/static/assets/img/'+f.name, 'wb+') as destination:
           for chunk in f.chunks():
               destination.write(chunk)
   ```

4. **`models.py`**  
   - Defines the database schema for all entities such as `Customer`, `Product`, `Order`, `Cart`, `Appointment`, and more.  
   - Example:
   ```python
   class customer(models.Model):
       c_id = models.AutoField(primary_key=True)
       c_name = models.CharField(max_length=20)
       c_email = models.EmailField(unique=True)
       c_contact = models.CharField(max_length=20)
       c_address = models.CharField(max_length=200)
       c_password = models.CharField(max_length=20)
       is_admin = models.IntegerField()
       area_id = models.ForeignKey(area, on_delete=models.CASCADE)
   ```

---


### **Project File (`manage.py`)**
- Main entry point for the Django project.
- Used to run servers, create migrations, and manage the project.

---

### **Database File (`petparadise.sql`)**
- Contains the SQL schema for setting up the project database, including initial data for entities.

---

## Setup Instructions

### 1. Prerequisites
- Python 3.8+ installed.
- Django 4.2+ installed.
- PostgreSQL or MySQL for the database.
- Install required Python packages:
  ```bash
  pip install -r requirements.txt
  ```

### 2. Clone the Repository
```bash
git clone <repository_url>
cd happypawpetstore
```

### 3. Set Up the Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 4. Import the Database
- Use the `petparadise.sql` file to set up your database:
  ```bash
  psql -U <username> -d <database_name> -f petparadise.sql
  ```
- Update `DATABASES` in `settings.py` with your database credentials.

### 5. Run Migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

### 6. Start the Development Server
```bash
python manage.py runserver
```

---

## Usage

1. **Admin Access**  
   - Visit `http://127.0.0.1:8000/admin` for the admin panel.
   - Use superuser credentials created during setup.

2. **Client Access**  
   - Visit `http://127.0.0.1:8000/` to explore the client-side interface.

---

## Technologies Used

- **Backend**: Django (Python)
- **Frontend**: HTML, CSS, JavaScript
- **Database**: PostgreSQL or MySQL
- **Media Storage**: Local storage in `happypawpetstore_Admin/static/assets`.

---

## Database Schema

### Key Tables
- `customer`: Manages customer details.
- `product`: Stores product information.
- `order`: Tracks orders placed by customers.
- `appointment`: Manages bookings with veterinarians.
- `feedback`: Handles customer reviews and ratings.
- `area`, `category`, `sub_category`: Provide organization for products and customer locations.

---

## Troubleshooting

### Common Issues
1. **Database Connection Errors**
   - Verify database credentials in `settings.py`.
   - Ensure the database server is running.

2. **Static Files Not Loading**
   - Run `python manage.py collectstatic`.
   - Check the `STATIC_ROOT` configuration in `settings.py`.

3. **Migration Issues**
   - Run `python manage.py makemigrations` and `python manage.py migrate` to sync models with the database.

---

## Future Enhancements

1. Add a payment gateway for online transactions.
2. Improve UI/UX for a more modern and responsive design.
3. Integrate notifications for orders and appointments.
4. Add support for multiple languages.

---

## Contributing

1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature-name
   ```
3. Commit changes and push to your forked repository.
4. Submit a pull request.

---

