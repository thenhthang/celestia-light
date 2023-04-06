# celestia-light

GUIDE for Submitting PayForBlob Transactions
Server Configuration
1. Install nginx as reverse proxy
installation information
server {
     server_name celestia.xn--radi-tqa.vn;
     location /celestia/pfb {
        proxy_pass http://localhost:26659/submit_pfb;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;

         # Headers to disable CORS
         add_header 'Access-Control-Allow-Origin' '*' always;
         add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS' always;
         add_header 'Access-Control-Allow-Headers' 'Authorization, Content-Type' always;
         if ($request_method = 'OPTIONS') {
             add_header 'Access-Control-Allow-Origin' '*';
             add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
             add_header 'Access-Control-Allow-Headers' 'Authorization, Content-Type';
             add_header 'Content-Length' 0;
             return 204;
         }
     }
     location /celestia/shares {
     proxy_pass http://localhost:26659/namespaced_shares;
     proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;

         # Headers to disable CORS
         add_header 'Access-Control-Allow-Origin' '*' always;
         add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS' always;
         add_header 'Access-Control-Allow-Headers' 'Authorization, Content-Type' always;
         if ($request_method = 'OPTIONS') {
             add_header 'Access-Control-Allow-Origin' '*';
             add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
             add_header 'Access-Control-Allow-Headers' 'Authorization, Content-Type';
             add_header 'Content-Length' 0;
             return 204;
         }
     }
     listen 443 ssl; # managed by Certbot
     ssl_certificate /etc/letsencrypt/live/celestia.xn--radi-tqa.vn/fullchain.pem; # managed by Certbot
     ssl_certificate_key /etc/letsencrypt/live/celestia.xn--radi-tqa.vn/privkey.pem; # managed by Certbot
     include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
     ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}
2. Configure https
sudo apt install certbot -y python3-certbot-nginx
certbot --nginx -d celestia.xn--radi-tqa.vn
