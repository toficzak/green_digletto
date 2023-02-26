Application is currently published on basic AWS free tier VPS.

http://ec2-52-3-19-153.compute-1.amazonaws.com

@toficzak will be taking care of cloud infrastructure.

There is one VPS - Instance of EC2 active.
It is Ubuntu server with Docker and Nginx installed.

Application executed:
``` shell
docker run -d --name green_digletto -p 8080:8080 --restart unless-stopped toficzak/green_digletto:0.0.1
```

Nginx config:
``` shell
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /var/www/html;

	index index.html index.htm index.nginx-debian.html;

	server_name ec2-52-3-19-153.compute-1.amazonaws.com 52.3.19.153;

	location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
		#try_files $uri $uri/ =404;
		proxy_pass http://127.0.0.1:8080;
		include proxy_params;
	}
}

```