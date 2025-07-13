# Super Organizer Database

PostgreSQL database implementation for the Super Organizer API - a comprehensive task management system.

## 🗄️ Overview

This repository contains the PostgreSQL database schema, sample data, and deployment configuration for the Super Organizer API. The database is designed to support a full-featured task management application with CRUD operations, search capabilities, and performance optimizations.

## 📋 Features

- **Complete PostgreSQL Schema** with custom ENUM types
- **Performance Optimized** with 8 strategic indexes
- **Data Integrity** with constraints and validations
- **Automatic Timestamp Management** with triggers
- **Docker Compose Setup** for easy deployment
- **Sample Data** for testing and development
- **Comprehensive Documentation** and setup guides

## 🚀 Quick Start

### Prerequisites
- Docker
- Docker Compose

### Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/CherepinRO/my_organizer_db.git
   cd my_organizer_db
   ```

2. **Start the database:**
   ```bash
   ./setup_postgres.sh
   ```

3. **Access the database:**
   - **PostgreSQL**: `localhost:5432`
   - **pgAdmin**: `http://localhost:8080`

### Connection Details
- **Database**: `super_organizer_db`
- **Username**: `postgres`
- **Password**: `password`
- **Host**: `localhost`
- **Port**: `5432`

## 📊 Database Structure

### Main Table: `tasks`

| Column | Type | Description |
|--------|------|-------------|
| id | BIGSERIAL | Primary key |
| date | DATE | Task date (required) |
| task_name | VARCHAR(255) | Task name (required) |
| comment | TEXT | Optional comment |
| deadline | TIMESTAMP | Optional deadline |
| priority | ENUM | HIGH, MEDIUM, LOW |
| task_type | ENUM | WORK, HOME |
| created_at | TIMESTAMP | Auto-generated |
| updated_at | TIMESTAMP | Auto-updated |

### ENUM Types
- **priority_enum**: `HIGH`, `MEDIUM`, `LOW`
- **task_type_enum**: `WORK`, `HOME`

## 🔧 Files Structure

```
my_organizer_db/
├── database/
│   ├── README.md                    # Database setup guide
│   ├── schema.sql                   # Complete schema
│   ├── sample_data.sql              # Sample data
│   └── migrations/
│       └── V1__Initial_schema.sql   # Migration script
├── docker-compose.yml               # Docker setup
├── setup_postgres.sh                # Automated setup
├── POSTGRESQL_DATABASE_IMPLEMENTATION.md  # Detailed implementation
└── README.md                        # This file
```

## 🛠️ Usage

### With Docker Compose

```bash
# Start PostgreSQL and pgAdmin
docker-compose up -d

# Stop services
docker-compose down

# Remove all data
docker-compose down -v
```

### Manual Setup

```bash
# Create database
createdb -U postgres super_organizer_db

# Apply schema
psql -U postgres -d super_organizer_db -f database/schema.sql

# Load sample data
psql -U postgres -d super_organizer_db -f database/sample_data.sql
```

## 🔍 Sample Queries

```sql
-- Get all tasks
SELECT * FROM tasks ORDER BY priority DESC, date ASC;

-- Get high priority tasks
SELECT * FROM tasks WHERE priority = 'HIGH';

-- Get tasks with deadlines
SELECT * FROM tasks WHERE deadline IS NOT NULL ORDER BY deadline ASC;

-- Search tasks by name
SELECT * FROM tasks WHERE task_name ILIKE '%project%';
```

## 📈 Performance Features

- **8 Strategic Indexes** for optimal query performance
- **Composite Indexes** for multi-column searches
- **Automatic Timestamp Updates** via triggers
- **Data Validation** with check constraints

## 🔐 Security

For production use:
- Change default passwords
- Use environment variables for credentials
- Enable SSL/TLS connections
- Set up proper user permissions

## 📚 Documentation

- **[Database README](database/README.md)**: Comprehensive setup guide
- **[Implementation Details](POSTGRESQL_DATABASE_IMPLEMENTATION.md)**: Complete implementation documentation

## 🤝 Integration

This database is designed to work with the [Super Organizer API](https://github.com/CherepinRO/my_organizer_api). To connect your Spring Boot application:

1. Add PostgreSQL dependency to `build.gradle.kts`
2. Configure `application-postgres.yml` with connection details
3. Run with profile: `--spring.profiles.active=postgres`

## 🧪 Testing

The database includes sample data for testing:
- 10 sample tasks with various priorities and types
- Tasks with and without deadlines
- Different dates and comments

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Related Projects

- **[Super Organizer API](https://github.com/CherepinRO/my_organizer_api)**: REST API application
- **[Super Organizer Frontend](https://github.com/CherepinRO/my_organizer_frontend)**: Web interface (if available)

---

**Ready to use!** Run `./setup_postgres.sh` to get started with the PostgreSQL database.