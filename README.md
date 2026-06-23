# Inventory Management System

A full-stack inventory management application built with FastAPI (backend) and React/Vite (frontend).

## Project Structure

```
inventory-management-system/
├── backend/          # FastAPI backend
│   ├── app/
│   │   ├── main.py
│   │   ├── models.py
│   │   ├── schemas.py
│   │   └── database.py
│   ├── requirements.txt
│   └── Dockerfile
└── frontend/         # React + Vite frontend
    ├── src/
    ├── package.json
    ├── vite.config.js
    └── Dockerfile
```

## Tech Stack

- **Backend**: FastAPI, SQLAlchemy, PostgreSQL
- **Frontend**: React 19, Vite, Material-UI (MUI), Axios
- **Database**: PostgreSQL
- **Deployment**: Docker, Render

## Local Development Setup

### Backend

```bash
cd inventory-management-system/backend
python -m venv venv
venv\Scripts\activate  # Windows
source venv/bin/activate  # macOS/Linux

pip install -r requirements.txt

# Create .env file
cp .env.example .env
# Update DATABASE_URL in .env

uvicorn app.main:app --reload
```

Backend runs on: `http://localhost:8000`

### Frontend

```bash
cd inventory-management-system/frontend
npm install

# Create .env file
cp .env.example .env
# Update VITE_API_BASE_URL if needed

npm run dev
```

Frontend runs on: `http://localhost:5173`

## Environment Variables

### Backend (.env)
```
DATABASE_URL=postgresql://user:password@localhost/inventory_db
FRONTEND_URL=http://localhost:5173
```

### Frontend (.env)
```
VITE_API_BASE_URL=http://localhost:8000
```

## API Endpoints

### Products
- `POST /products` - Create product
- `GET /products` - Get all products
- `GET /products/{product_id}` - Get product details
- `PUT /products/{product_id}` - Update product
- `DELETE /products/{product_id}` - Delete product

### Customers
- `POST /customers` - Create customer
- `GET /customers` - Get all customers
- `GET /customers/{customer_id}` - Get customer details
- `PUT /customers/{customer_id}` - Update customer
- `DELETE /customers/{customer_id}` - Delete customer

### Orders
- `POST /orders` - Create order
- `GET /orders` - Get all orders
- `GET /orders/{order_id}` - Get order details
- `PUT /orders/{order_id}` - Update order
- `DELETE /orders/{order_id}` - Delete order

## Deployment on Render

See [RENDER_DEPLOYMENT_GUIDE.md](RENDER_DEPLOYMENT_GUIDE.md) for complete deployment instructions.

Quick steps:
1. Push code to GitHub
2. Create PostgreSQL database on Render
3. Deploy backend service
4. Deploy frontend service
5. Configure environment variables

## License

MIT
