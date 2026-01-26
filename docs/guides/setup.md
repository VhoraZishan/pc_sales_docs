# Local Development Setup

Follow this guide to set up the **Parul Chemicals Sales (pc_sales)** application locally.

## Prerequisites
- **Git**: Installed and configured.
- **Python 3.12**: **Recommended for Windows Development**.
    - *Note*: This is not a strict production requirement, but highly recommended for Windows to avoid dependency installation issues (e.g., missing wheels for certain packages).
- **Node.js**: LTS version (v18+ recommended).

## 1. Clone the Repository
Start by getting the code from GitHub.

```powershell
# Open your terminal in the directory where you want the project
git clone https://github.com/yashdave182/pc_sales.git

# Move into the project directory
cd pc_sales
```

## 2. Environment Configuration
> 🛑 **Review Step**: The application requires separate environment variables for the frontend and backend.
> **Action**: Contact the Product Manager to acquire the specific `.env` files for both.

1.  **Backend**: Place the backend `.env` file inside `backend/`.
2.  **Frontend**: Place the frontend `.env` file inside `frontend/`.

## 3. Backend Setup
The backend uses **FastAPI**.

```powershell
# 1. Navigate to the backend folder
cd backend

# 2. Create the virtual environment (Python 3.12 recommended for Windows)
# If 'python' is not 3.12, use 'py -3.12' or the specific command for your installation
python -m venv venv

# 3. Activate the virtual environment
# Windows:
.\venv\Scripts\Activate
# Linux/Mac:
# source venv/bin/activate

# 4. Install dependencies
pip install -r requirements.txt
```
*Troubleshooting*: If you see errors about "building wheels" on Windows, it is likely a Python version mismatch. Switching to Python 3.12 usually resolves this.

## 4. Frontend Setup
The frontend is built with **React JS** (Vite).

```powershell
# 1. Open a new terminal and navigate to the root, then frontend
cd frontend

# 2. Install Node dependencies
npm install
```

## 5. Running the Application

### Start the Backend
```powershell
# In the backend terminal (with venv activated):
uvicorn main:app --reload
```
API will launch at: `http://localhost:8000`

### Start the Frontend
```powershell
# In the frontend terminal:
npm run dev
```
UI will launch at: `http://localhost:5173` (typically).

## 6. Verification
- **Frontend**: Go to `http://localhost:5173`. You should see the login screen.
- **Backend Specs**: Go to `http://localhost:8000/docs`. You should see the Swagger UI.
