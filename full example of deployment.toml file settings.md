Here’s a full example of a `deployment.toml` file with common settings configured for WSO2 API Manager. This includes configurations for server hostname, port settings, database configurations, and analytics. You can adapt this template based on your environment and requirements.

### Example `deployment.toml` File:

```toml
# General server configurations
[server]
hostname = "localhost"
node_ip = "127.0.0.1"
mode = "single_node"
http_port = 9763
https_port = 9443
# offset = 0 # Set this if you want to run multiple WSO2 instances on the same host

[super_admin]
username = "admin"
password = "admin"
create_admin_account = true

# Database configurations for API Manager's main database (APIM_DB)
[database.apim_db]
type = "mysql" # or "postgresql", "oracle", "mssql"
url = "jdbc:mysql://localhost:3306/apim_db"
username = "apim_user"
password = "apim_password"
driver = "com.mysql.cj.jdbc.Driver"
validationQuery = "SELECT 1"

# Database configurations for User Management (UM_DB)
[database.shared_db]
type = "mysql"
url = "jdbc:mysql://localhost:3306/shared_db"
username = "shared_user"
password = "shared_password"
driver = "com.mysql.cj.jdbc.Driver"
validationQuery = "SELECT 1"

# Throttling Database (Optional)
[database.throttling_db]
type = "mysql"
url = "jdbc:mysql://localhost:3306/throttling_db"
username = "throttling_user"
password = "throttling_password"
driver = "com.mysql.cj.jdbc.Driver"
validationQuery = "SELECT 1"

# Registry database configuration (Optional, for governance, etc.)
[database.registry_db]
type = "mysql"
url = "jdbc:mysql://localhost:3306/registry_db"
username = "registry_user"
password = "registry_password"
driver = "com.mysql.cj.jdbc.Driver"
validationQuery = "SELECT 1"

# Gateway environment configurations
[[apim.gateway.environment]]
name = "Production and Sandbox"
type = "hybrid"
display_in_api_console = true
description = "Default gateway"
service_url = "https://localhost:9443/services/"
username = "admin"
password = "admin"

# CORS configuration for APIs
[cors]
enabled = true
allow_origins = "*"
allow_methods = ["GET", "POST", "DELETE", "PUT", "OPTIONS", "PATCH"]
allow_headers = ["authorization", "Access-Control-Allow-Origin", "Content-Type"]
allow_credentials = false

# Analytics configurations (WSO2 API Manager Analytics)
[apim.analytics]
enable = true
server_url = "https://localhost:9444"
auth_url = "https://localhost:9445"
username = "admin"
password = "admin"

# Identity Provider (IDP) settings (Key Manager)
[apim.key_manager]
server_url = "https://localhost:9443/services/"
username = "admin"
password = "admin"

# JWT token configurations
[apim.jwt]
enable = true
token_expiry = 3600
# Set claims, signing algorithms, etc.

# Configurations for OAuth token validation
[apim.oauth]
enable = true
token_url = "https://localhost:8243/token"
introspect_url = "https://localhost:8243/oauth2/introspect"
client_id = "sample-client-id"
client_secret = "sample-client-secret"

# Throttling configurations
[apim.throttling]
enable = true
url = "https://localhost:9443/throttling-service"
username = "admin"
password = "admin"

# Email Sender Configurations
[email.sender]
email = "noreply@yourdomain.com"
username = "emailuser"
password = "emailpassword"
host = "smtp.yourdomain.com"
port = 587
from_address = "noreply@yourdomain.com"
enable_starttls = true
enable_authentication = true

# External Cache Configuration (for throttling, etc.)
[cache.external_cache]
enable = true
host = "localhost"
port = 6379

# Logging configuration
[logging]
log_level = "INFO"
file_path = "${carbon.home}/repository/logs/wso2carbon.log"
log_file_rotate_interval = "daily"
max_retained_backups = 30

# HSTS (HTTP Strict Transport Security) settings (for HTTPS)
[security.headers]
strict_transport_security.enable = true
strict_transport_security.max_age = 31536000
strict_transport_security.include_subdomains = true
```

### Key Configurations Explained:

1. **[server]**: Basic server configurations like hostname, IP, and ports.
   - `hostname`: Hostname of your server.
   - `http_port`/`https_port`: Default HTTP/HTTPS ports.

2. **[super_admin]**: Defines the super admin user (default username and password).

3. **Database Configurations**:
   - **[database.apim_db]**: Main API Manager database.
   - **[database.shared_db]**: Database used for user management.
   - **[database.throttling_db]**: Optional throttling database.
   - **[database.registry_db]**: Optional registry database.
   - These include fields like `type` (the database type), `url`, and `credentials`.

4. **[apim.gateway.environment]**: Configuration for the API Gateway environment.

5. **[cors]**: Cross-Origin Resource Sharing configuration to allow client applications to interact with your API.

6. **[apim.analytics]**: Configures integration with the WSO2 Analytics component for monitoring and reporting API usage.

7. **[apim.key_manager]**: The key manager handles token validation and OAuth operations.

8. **[apim.jwt]**: Enables and configures JWT tokens for API authentication.

9. **[apim.oauth]**: OAuth settings for client and introspection URLs.

10. **[apim.throttling]**: Configures API throttling policies and service endpoints.

11. **[email.sender]**: Configurations for the email server used for notifications, alerts, etc.

12. **[cache.external_cache]**: External cache configuration, like Redis, for performance improvement in throttling and other use cases.

13. **[logging]**: Log file configuration, log levels, and retention policies.

14. **[security.headers]**: HSTS headers for improved security, particularly in HTTPS environments.

### Customization Based on Environment:

- **Production Setup**: Replace the `localhost` with the actual server's hostname or IP.
- **Database**: Use external databases like MySQL or PostgreSQL for production instead of the default H2 database.
- **Clustering**: In a clustered environment, more advanced configurations would be required, such as distributed caching, load balancing, and high-availability settings.

You can add or modify other sections depending on your organization's requirements, such as enabling specific security policies, configuring additional gateway environments, or tweaking logging levels.