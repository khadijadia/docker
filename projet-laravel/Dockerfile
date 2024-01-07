
# Utiliser l'image officielle PHP avec Apache basée sur PHP 8.1
FROM php:8.1.2-apache

# Installer les dépendances nécessaires
RUN apt-get update && \
    apt-get install -y libzip-dev zip && \
    docker-php-ext-configure zip && \
    docker-php-ext-install zip pdo_mysql && \
    a2enmod rewrite

# Installer Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Définir le répertoire de travail
WORKDIR /var/www

# Copier les fichiers de l'application Laravel dans le conteneur
COPY . .

# Installer les dépendances de l'application Laravel
RUN cd /var/www/ && \
    composer install

# Définir l'environnement Laravel
ENV APACHE_DOCUMENT_ROOT /var/www/html/public
ENV APACHE_LOG_DIR /var/log/apache2

# Configurer le fichier de virtual host d'Apache
COPY laravel.conf /etc/apache2/sites-available/000-default.conf

# Exposer le port 80
EXPOSE 80

# Démarrer Apache
CMD ["apache2-foreground"]
