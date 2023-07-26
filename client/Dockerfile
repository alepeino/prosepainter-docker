FROM node:14.21.3-alpine as builder

WORKDIR /app

RUN apk add --upgrade git

# Clone ProsePainter repo
RUN git clone https://github.com/Morphogens/ProsePainter.git

WORKDIR ProsePainter/client

# Install ProsePainter client deps
RUN npm install

# Build ProsePainter client
RUN npm run build

FROM nginx:alpine
WORKDIR /app
RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /app/ProsePainter/client/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
