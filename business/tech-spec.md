```markdown
# Technical Specification: fund-comply

## Stack
- **Language**: Python (FastAPI for backend), JavaScript (React for frontend)
- **Database**: PostgreSQL (for relational data), MongoDB (for unstructured data)
- **Hosting**: AWS (free-tier-first: EC2 for backend, S3 for storage, RDS for PostgreSQL, DocumentDB for MongoDB)
- **Containerization**: Docker
- **Orchestration**: Kubernetes

## Data Model
### Tables/Collections
1. **Users**
   - `id` (UUID, primary key)
   - `email` (String, unique)
   - `password_hash` (String)
   - `role` (String, e.g., 'admin', 'user')
   - `created_at` (Timestamp)
   - `updated_at` (Timestamp)

2. **Funds**
   - `id` (UUID, primary key)
   - `name` (String)
   - `description` (Text)
   - `type` (String, e.g., 'private equity', 'venture capital')
   - `created_at` (Timestamp)
   - `updated_at` (Timestamp)

3. **ComplianceDocuments**
   - `id` (UUID, primary key)
   - `fund_id` (UUID, foreign key to Funds)
   - `document_type` (String, e.g., 'KYC', 'AML')
   - `file_path` (String)
   - `uploaded_at` (Timestamp)
   - `status` (String, e.g., 'pending', 'approved', 'rejected')

4. **Reports**
   - `id` (UUID, primary key)
   - `fund_id` (UUID, foreign key to Funds)
   - `report_type` (String, e.g., 'quarterly', 'annual')
   - `file_path` (String)
   - `generated_at` (Timestamp)

## API Surface
1. **User Authentication**
   - `POST /auth/register` - Register a new user
   - `POST /auth/login` - Login a user
   - `POST /auth/logout` - Logout a user

2. **Fund Management**
   - `GET /funds` - List all funds
   - `POST /funds` - Create a new fund
   - `GET /funds/{fund_id}` - Get fund details
   - `PUT /funds/{fund_id}` - Update fund details
   - `DELETE /funds/{fund_id}` - Delete a fund

3. **Compliance Document Management**
   - `GET /funds/{fund_id}/documents` - List all compliance documents for a fund
   - `POST /funds/{fund_id}/documents` - Upload a compliance document
   - `GET /funds/{fund_id}/documents/{document_id}` - Get compliance document details
   - `PUT /funds/{fund_id}/documents/{document_id}` - Update compliance document status

4. **Report Generation**
   - `GET /funds/{fund_id}/reports` - List all reports for a fund
   - `POST /funds/{fund_id}/reports` - Generate a new report
   - `GET /funds/{fund_id}/reports/{report_id}` - Get report details

## Security Model
- **Authentication**: JWT (JSON Web Tokens)
- **Authorization**: Role-Based Access Control (RBAC)
- **Secrets Management**: AWS Secrets Manager
- **IAM**: AWS IAM roles and policies for different services

## Observability
- **Logging**: AWS CloudWatch Logs
- **Metrics**: AWS CloudWatch Metrics
- **Traces**: AWS X-Ray

## Build/CI
- **Build Tool**: Docker
- **CI/CD**: AWS CodePipeline
- **Testing**: Pytest (backend), Jest (frontend)
- **Code Quality**: SonarQube
- **Security Scanning**: Postman (API security testing)
```