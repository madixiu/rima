# build stage
# Use an official Node runtime as the base image
FROM node:20.14-alpine as build-stage

# Set the working directory in the container
WORKDIR /client

# Install Yarn
# RUN npm install -g yarn

# Copy the package.json and package-lock.json to the current directory
COPY ../frontend/package.json ./

# RUN npm cache verify
COPY ../frontend/ .

# Install any needed packages specified in package-json
RUN yarn install


# Run the build script
RUN yarn run build

# production stage
FROM nginx:1.24.0 as production-stage

COPY --from=build-stage /client/build /usr/share/nginx/html

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]