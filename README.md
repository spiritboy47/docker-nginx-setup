# docker-nginx-setup

# 🚀 docker-nginx-setup

A minimal and flexible **NGINX setup using Docker Compose**. Supports SSL, virtual hosts via `conf.d`, project-based HTML directory structure, and logs.

---

## 📦 What's Inside

```bash
.
├── docker-compose.yml       # Docker Compose setup for NGINX
├── conf.d/                  # NGINX site configurations (server blocks)
│   └── default.conf         # Sample config file
├── ssl/                     # SSL certificates
│   ├── example.crt
│   └── example.key
├── html/                    # Web root for your projects
│   └── project1/
│       └── index.html
├── logs/                    # Logs for NGINX
│   ├── access.log
│   └── error.log


⚙️ **How It Works**
* NGINX is deployed in a Docker container.
* Uses conf.d/ for custom server blocks (virtual hosts).
* SSL-ready via mounted certs in ssl/.
* All static content/projects go under html/.
* Logs are saved in logs/.

🧾 **Sample Configuration (conf.d/default.conf)**
server {
    listen 80;
    server_name localhost;

    root /var/www/html/project1;
    index index.html;

    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;

    location / {
        try_files $uri $uri/ =404;
    }
}


🛠️ **How to Use**
1. Clone the repo
git clone https://github.com/yourusername/docker-nginx-setup.git
cd docker-nginx-setup

2. Add your project(s)
Place your web files under html/project-name/
Update the corresponding config in conf.d/

3. (Optional) Add SSL certificates
Put your .crt and .key files under ssl/
Update your server block to listen on port 443

4. Run it
docker-compose up -d

5. View logs
docker logs nginx


📍 **Notes**
You can add multiple server blocks for different domains in the conf.d/ directory.
The monitoring_network is a named Docker bridge network; you can attach other containers (like apps or monitoring tools) to this for integration.

🧪 **Tested On**
Docker: 24+
Docker Compose: v2+
NGINX: latest
