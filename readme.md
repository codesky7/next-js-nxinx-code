sudo nano /etc/nginx/sites-available/graphifyai.conf

sudo ln -s /etc/nginx/sites-available/graphifyai.conf /etc/nginx/sites-enabled/



server {
    listen 80;
    server_name graphifyai.com www.graphifyai.com;

    # Redirect HTTP to HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name graphifyai.com www.graphifyai.com;

    ssl_certificate /etc/letsencrypt/live/graphifyai.com/fullchain.pem; 
    ssl_certificate_key /etc/letsencrypt/live/graphifyai.com/privkey.pem; 

    location / {
        # Your existing location configuration
        proxy_pass http://localhost:3000;  
        # Other proxy settings
    }
}
