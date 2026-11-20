
FROM makeplane/plane-aio-community:v1.4.3

# Logs visibles en Railway y configuración inicial
COPY supervisor.conf /etc/supervisor/conf.d/supervisor.conf
COPY railway_setup.py /app/backend/plane/db/management/commands/railway_setup.py

# Redirigir dominios de Railway al dominio personalizado
RUN printf '\nhttp://*.up.railway.app {\n    redir https://{$CUSTOM_DOMAIN}{uri} permanent\n}\n' >> /app/proxy/Caddyfile

# Personalización visual de Plane
RUN find /app/web /app/space -type f -name "*.css" \
    ! -path "*/node_modules/*" \
    -exec sh -c 'printf "\n\
/* Ocultar enlaces de GitHub */\n\
a[href*=\"://github.com\"] {\n\
    display: none !important;\n\
}\n\
/* Ocultar Community y version del sidebar */\n\
div.h-12.border-t:has(button[aria-haspopup=\"dialog\"][aria-label*=\"paid plans\" i]),\n\
div.h-12.border-t:has(button[aria-haspopup=\"dialog\"][aria-label*=\"planes de pago\" i]) {\n\
    display: none !important;\n\
}\n" >> "$1"' _ {} \;
