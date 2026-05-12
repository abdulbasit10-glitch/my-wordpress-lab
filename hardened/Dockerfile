# Use latest WordPress (NOT old 5.8!)
FROM wordpress:latest

# Switch to root to install updates
USER root

# Update everything to latest versions!
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y curl && \
    apt-get clean

# Remove dangerous tools that attackers could use
RUN apt-get remove -y --purge gcc make && \
    apt-get autoremove -y

# Create a NON-ROOT user (super important!)
RUN adduser --disabled-password --gecos '' wordpress-user

# Fix permissions for safe running
RUN chown -R wordpress-user:wordpress-user /var/www/html

# Switch to safe user (not root!)
USER wordpress-user

# Add health check
HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
  CMD curl -f http://localhost/ || exit 1
