# build stage
# Use an official Node runtime as the base image
FROM node:lts-alpine as build-stage

# Set the working directory in the container
WORKDIR /frontend/

# Install Yarn
RUN npm install -g yarn

# Copy the package.json and package-lock.json to the current directory
COPY frontend/package.json /frontend/

# RUN npm cache verify

# Install any needed packages specified in package-json
RUN yarn install

COPY frontend /frontend/

# Run the build script
RUN yarn run build

# production stage
FROM nginx:stable-alpine as production-stage
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=build-stage /frontend/build /build/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]