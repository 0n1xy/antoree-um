# # Sử dụng image PHP chính thức có Composer
# FROM php:8.2-fpm

# # Cài đặt các dependencies cần thiết
# RUN apt-get update && apt-get install -y \
#     git \
#     unzip \
#     netcat-openbsd \
#     && docker-php-ext-install pdo_mysql

# # Cài đặt Composer
# COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# # Thiết lập thư mục làm việc
# WORKDIR /var/www

# # Copy file dự án vào container
# COPY . .

# # Cài đặt các gói Composer cho Laravel
# RUN composer install --no-dev --optimize-autoloader

# # Tạo khóa ứng dụng, chạy migrate và seed database, tạo JWT secret
# RUN php artisan key:generate && \
#     php artisan migrate --seed --force && \
#     php artisan jwt:secret --force

# # Thiết lập quyền cho thư mục storage & bootstrap/cache
# RUN chmod -R 775 storage bootstrap/cache && chown -R www-data:www-data storage bootstrap/cache

# # Expose port của container
# EXPOSE 9000

# # Chạy PHP-FPM ngay lập tức
# CMD ["php-fpm"]

# Sử dụng image PHP chính thức có Composer
FROM php:8.2-fpm

# Cài đặt các dependencies cần thiết
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    netcat-openbsd \
    && docker-php-ext-install pdo_mysql

# Cài đặt Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Thiết lập thư mục làm việc
WORKDIR /var/www

# Copy file dự án vào container
COPY . .

# Cài đặt các gói Composer cho Laravel
RUN composer install --no-dev --optimize-autoloader

# Thiết lập quyền cho thư mục storage & bootstrap/cache
RUN chmod -R 775 storage bootstrap/cache && chown -R www-data:www-data storage bootstrap/cache

# Copy entrypoint script
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Expose port của container
EXPOSE 9000

# Sử dụng entrypoint.sh thay vì chạy PHP-FPM trực tiếp
ENTRYPOINT ["/entrypoint.sh"]
