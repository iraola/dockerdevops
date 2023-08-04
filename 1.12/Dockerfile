FROM ubuntu

WORKDIR /usr/src/app

COPY . .
 
# Install node
RUN apt update
RUN apt install -y nodejs
RUN apt install -y npm

# Expose port
EXPOSE 5000

# Build project
RUN npm install
RUN npm run build
RUN npm install -g serve

# Run frontend
CMD ["serve", "-s", "-l", "5000", "build"]

