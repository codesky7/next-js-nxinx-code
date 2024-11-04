sudo nano /etc/nginx/sites-available/graphifyai.conf

sudo ln -s /etc/nginx/sites-available/graphifyai.conf /etc/nginx/sites-enabled/



server {
    listen 443 ssl;
    server_name graphifyai.com www.graphifyai.com;

    ssl_certificate /etc/letsencrypt/live/graphifyai.com/fullchain.pem; 
    ssl_certificate_key /etc/letsencrypt/live/graphifyai.com/privkey.pem; 

location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}
