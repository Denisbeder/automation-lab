# Automation Lab

A containerized environment for workflow automation and WhatsApp integration using n8n and Evolution API.

## 🚀 Features

- **n8n**: Workflow automation platform
- **Evolution API**: WhatsApp Business API
- **PostgreSQL**: Database for data persistence
- **Redis**: Caching layer (optional)
- **ngrok**: Secure tunnels to localhost for testing

## 🛠 Prerequisites

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [ngrok account](https://ngrok.com/) (for webhook testing)

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd automation-lab
   ```

2. **Configure environment variables**
   ```bash
   cp .env.example .env
   ```
   Update the `.env` file with your configuration:
   - Set your PostgreSQL credentials
   - Configure n8n authentication
   - Set Evolution API authentication key
   - Configure Redis if needed

3. **Configure ngrok**
   - Sign up at [ngrok](https://ngrok.com/)
   - Get your authtoken
   - Update `ngrok.yml` with your authtoken

4. **Start the services**
   ```bash
   docker-compose up -d
   ```

5. **Access the services**
   - n8n: http://localhost:5678
   - Evolution API: http://localhost:8080
   - ngrok Web Interface: http://localhost:4040

## 🔧 Services

- **n8n**: Workflow automation tool
  - Port: 5678
  - Default credentials (change these in `.env`):
    - Email: admin@email.com
    - Password: Abc123!

- **Evolution API**: WhatsApp Business API
  - Port: 8080
  - API Key: Configured in `.env`

- **PostgreSQL**: Database
  - Port: 5432
  - Credentials configured in `.env`

- **Redis**: Caching (disabled by default)
  - Port: 6379

- **ngrok**: Secure tunnels
  - Web Interface: 4040
  - Creates public URLs for local services

## 🌐 Webhook Configuration

To receive webhooks from external services:

1. Start ngrok with `docker-compose up -d ngrok`
2. Check the ngrok web interface at http://localhost:4040 for your public URLs
3. Use these URLs to configure webhooks in external services
4. Since this project uses Ngrok, the public URL generated for n8n changes every time the services are restarted. You will need to:
Go to http://localhost:4040 to get the new Ngrok URL (example: https://abcd-1234.ngrok.io).
Update the webhook URL in the Evolution API (usually in your integration settings or endpoints).
If you have configured webhooks in other n8n services or flows that depend on this URL, update them as well.
Reminder: Always reset the webhook URLs after restarting the services to ensure everything works properly.

## 🔒 Security Notes

- Change all default credentials before deploying to production
- Use strong passwords for all services
- Configure proper firewall rules
- Enable HTTPS for production use
- Regularly update the Docker images
