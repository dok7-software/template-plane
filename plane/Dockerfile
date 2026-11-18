FROM makeplane/plane-aio-community:v1.4.3
# Same programs as upstream, but logging to stdout so Railway shows them
# (upstream writes everything to files under /app/logs), plus the admin setup.
COPY supervisor.conf /etc/supervisor/conf.d/supervisor.conf
COPY railway_setup.py /app/backend/plane/db/management/commands/railway_setup.py

# Añade la redirección desde cualquier subdominio de Railway hacia tu dominio custom
RUN printf '\nhttp://*.up.railway.app {\n    redir https://{$CUSTOM_DOMAIN}{uri} permanent\n}\n' >> /app/proxy/Caddyfile

# Inyecta una regla CSS global en los archivos compilados para ocultar el botón de GitHub
RUN find /app/web /app/space -type f -name "*.css" \
    ! -path "*/node_modules/*" \
    -exec sh -c 'printf "\na[href*=\"://github.com\"] { display: none !important; }\n" >> "$1"' _ {} \;
