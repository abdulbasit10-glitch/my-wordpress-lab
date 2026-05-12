# Latest WordPress use karo (safe wala)
FROM wordpress:latest

# Root ban ke update karo
USER root

# Sab kuch update karo
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y curl && \
    apt-get clean

# Dangerous tools hatao
RUN apt-get remove -y --purge gcc make && \
    apt-get autoremove -y

# Naya safe user banao (not root!)
RUN adduser --disabled-password --gecos '' wordpress-user

# Permissions fix karo
RUN chown -R wordpress-user:wordpress-user /var/www/html

# Safe user pe switch karo
USER wordpress-user

# Health check dalo (robot check karega sab theek hai)
HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
  CMD curl -f http://localhost/ || exit 1
