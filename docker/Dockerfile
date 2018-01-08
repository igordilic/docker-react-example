FROM igorilic/nginx-node-base:latest

# Working directory
ENV APP_DIR /usr/src/react-www

RUN mkdir -p $APP_DIR
WORKDIR $APP_DIR

# Copying mandatory files and tools
COPY ./package.json ./
COPY ./yarn.lock ./
COPY ./public ./public

# Ensure that node_modules are building from the scratch
RUN rm -rf ./node_modules

# Installing node modules
RUN yarn install

# Copy data
COPY . $APP_DIR

# Build an application
RUN yarn build

# Nginx setup
COPY docker/nginx/nginx.conf /etc/nginx/nginx.conf
COPY docker/nginx/default.conf /etc/nginx/conf.d/default.conf
RUN chmod +x /etc/nginx/conf.d/default.conf
RUN rm -rf /usr/share/nginx/html && \
    mkdir -p /usr/share/nginx/html && \
    ln -s $(pwd)/build /usr/share/nginx/html/react-www

EXPOSE 80
