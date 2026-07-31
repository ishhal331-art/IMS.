# Inventory Portal — Production Build

## Architecture
GitHub -> Render Node/Express API -> Supabase PostgreSQL. The frontend is served by the same Render service, so one permanent Render URL can be shared with users.

## Important
This build does NOT use db.json and does NOT seed sample products, suppliers, warehouses, transactions, or manager accounts. On first startup it creates the database schema and only creates an initial admin if none exists.

### Render environment variables
- DATABASE_URL = Supabase PostgreSQL connection string
- JWT_SECRET = long random secret
- ADMIN_USERNAME = desired initial admin username
- ADMIN_PASSWORD = strong initial admin password
- ADMIN_NAME = administrator display name
- FRONTEND_URL = public portal URL (optional for this build)

Do not commit secrets to GitHub.

## Supabase
Create a Supabase project, open Connect / Database, copy a PostgreSQL connection string, and place it in Render as DATABASE_URL. The application runs safe `CREATE TABLE IF NOT EXISTS` migrations on startup; it never drops tables or resets production data.

## Reports
Inventory and overall reports support PDF, CSV and Excel (XLSX), with optional start/end date filtering.

## Testing
Use a test Supabase project first. Create test users/products, sell stock, attempt to oversell, test notifications, reports and redeploy persistence before using production data.
