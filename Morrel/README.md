# 🏪 LocalFind — Local Store Directory

A full-featured local store directory web application built with Flask. Store owners can register and manage their stores (with map location pinning), and admins can approve listings, manage users, and customize the site's branding.

---

## ✨ Features

- **Authentication**: Register, Login, Logout with secure password hashing
- **Two Account Roles**:
  - **Store Owner** — Register and manage store listings
  - **Admin** — Full control over stores, users, and site settings
- **Google Maps Integration**:
  - 3-step store registration wizard with interactive map location picker
  - Autocomplete address search
  - Drag-to-adjust pin placement
  - Browse map showing all store locations
  - Store detail page with embedded map
- **Store Management**:
  - Upload store logo
  - Choose from 16 categories (Grocery, Pharmacy, Restaurant, etc.)
  - Add tags (24/7, Delivery, Parking, etc.)
  - Opening hours, contact info, website
  - Admin approval workflow before going live
- **Search & Filter**:
  - Text search by name, description, address
  - Filter by category
  - Filter by tag
  - Paginated results
- **Admin Panel**:
  - Dashboard with stats
  - Approve/reject/disable stores
  - Manage users (promote to admin, enable/disable)
  - Live site settings: name, tagline, colors, logo, Google Maps API key, footer text
- **Theme Customization**:
  - 5 color pickers with live preview
  - Upload site logo shown in navbar
  - Changes apply instantly across all pages via CSS variables

---

## 🚀 Quick Start

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Run the app

```bash
python app.py
```

Open your browser at **http://localhost:5000**

### 3. Default Admin Credentials

```
Username: admin
Password: admin1234
```

> ⚠️ **Change the admin password after first login!** Also change `SECRET_KEY` in `app.py` before deploying.

---

## 🗺 Map Setup

This app now uses Leaflet with OpenStreetMap tiles for map display and location picking. No Google Maps API key is required.

1. Start the application as usual.
2. Register or edit a store and use the address search field or click on the map to place the pin.
3. Browse stores and open store detail pages to see maps rendered with Leaflet.

> The site uses open map tiles from OpenStreetMap, so no external map provider key is required.

---

## 📁 Project Structure

```
store_directory/
├── app.py                     # Main Flask application & routes
├── requirements.txt
├── README.md
├── store_directory.db         # Created automatically on first run
├── static/
│   └── uploads/
│       ├── logos/             # Store logos
│       └── site/              # Site logo
└── templates/
    ├── base.html              # Layout with nav, flash messages, footer
    ├── index.html             # Homepage with hero, categories, featured stores
    ├── login.html
    ├── register.html
    ├── stores.html            # Browse + search + map view
    ├── store_detail.html      # Individual store page with map
    ├── add_store.html         # 3-step store registration with map picker
    ├── edit_store.html        # Edit store with map
    ├── dashboard_owner.html   # Store owner dashboard
    ├── admin_dashboard.html   # Admin overview
    ├── admin_stores.html      # Admin store management
    ├── admin_users.html       # Admin user management
    └── admin_settings.html    # Theme & site customization
```

---

## 🔐 User Roles

| Feature | Store Owner | Admin |
|---------|-------------|-------|
| Register/login | ✓ | ✓ |
| Add stores | ✓ | ✓ |
| Edit own stores | ✓ | ✓ |
| Delete own stores | ✓ | ✓ |
| View pending stores | Own only | All |
| Approve stores | ✗ | ✓ |
| Manage all stores | ✗ | ✓ |
| Manage users | ✗ | ✓ |
| Site settings | ✗ | ✓ |

---

## 🛠 Customization

- **Categories**: Edit the `CATEGORIES` list in `add_store()` and `edit_store()` routes
- **Tags**: Edit the `TAGS` list in those same routes
- **Database**: Swap SQLite for PostgreSQL by changing `SQLALCHEMY_DATABASE_URI`
- **Port**: Change `app.run(port=8000)` or use a WSGI server like Gunicorn

---

## 📦 Production Deployment

```bash
# Install gunicorn
pip install gunicorn

# Run with gunicorn
gunicorn -w 4 -b 0.0.0.0:8000 app:app
```

Remember to:
- Set `DEBUG=False`
- Use a strong `SECRET_KEY`
- Configure a proper database (PostgreSQL recommended)
- Set up file storage (AWS S3 or similar) for uploaded images
- Add HTTPS via a reverse proxy (nginx + certbot)
