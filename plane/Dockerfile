FROM makeplane/plane-aio-community:v1.4.3
# Same programs as upstream, but logging to stdout so Railway shows them
# (upstream writes everything to files under /app/logs), plus the admin setup.
COPY supervisor.conf /etc/supervisor/conf.d/supervisor.conf
COPY railway_setup.py /app/backend/plane/db/management/commands/railway_setup.py

# Añade la redirección desde cualquier subdominio de Railway hacia tu dominio custom
RUN sed -i '1i http://*.up.railway.app {\n    redir https://{$CUSTOM_DOMAIN}{uri} permanent\n}\n' /app/proxy/Caddyfile
