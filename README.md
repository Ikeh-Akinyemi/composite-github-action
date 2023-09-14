# Database Migration

This action performs database migration on a PostgreSQL service created for testing purposes.

## Inputs

### `database_url` (required)

The `db_url` connection string for the PostgreSQL database. The format is: `postgres://[user[:password]@][netloc][:port][/dbname][?param1=value1&...]`.

**Example:**
```
postgres://root:password@localhost:5432/test?sslmode=disable
```

### `migration_files_path` (required)

The file path to the migration files that contain SQL scripts for database migration.

**Example:**
```
db/migrations
```

## Outputs

### `migration_report`

This output provides a report on the status of the database migration.

**Example (Successful Migration):**
```
Migrated database successfully
```

**Example (Failed Migration):**
```
Failed to migrate database
```

## Usage

```yaml
jobs:
  migrate-database:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      
      - name: Run Database Migration
        id: migrate
        uses: your-username/database-migration-action@v1
        with:
          database_url: ${{ secrets.DATABASE_URL }}
          migration_files_path: db/migrations
      
      - name: Check Migration Status
        run: echo "Migration status: ${{ steps.migrate.outputs.migration_report }}"
```

This action performs database migration using the [golang-migrate](https://github.com/golang-migrate/migrate) tool. It installs the tool, applies migrations, and reports the migration status.