FROM node:16

WORKDIR /usr/src/app

COPY . .

# Expose port
EXPOSE 5000

# Set environment variable
ENV REACT_APP_BACKEND_URL=http://localhost:8080/

# Build project
RUN npm install
RUN npm run build
RUN npm install -g serve

# Run frontend
CMD ["serve", "-s", "-l", "5000", "build"]

