---
title: "Publishing Preserved Artifacts"
date: "14/04/2021"
aliases:
  - "/getting-started/publishing-preserved-artifacts/"
---

With the [CI task](/pipelines/tasks/ci) in a Code Stream Pipeline, it's possible to [Preserve Artifacts](/pipelines/tasks/ci/#preserve-artifacts) - any file that you want to persist beyond the lifetime of a [Pipeline Execution](/executions) can be added to the Preserve Artifacts field. These preserved artifacts are stored on the Shared Path on the [Docker Host](/configure/endpoints/docker), which you can access later using the file path specified in the CI task outputs. One of the issues with this is that the Shared Path is also where the pipeline execution logs are kept, which may contain sensitive information if you're not using [Secret Variables](/configure/variables), and to deliver a preserved file to an end user you may need to grant SSH access to your host - not ideal.

In order allow my end users to download a preserved artifact without granting them SSH access to my Docker host, I will publish the Shared Path using NGINX.

I've already got an SSL certificate and key (`cmbu.local.crt.pem` and `cmbu.local.key.pem`) to provide SSL access to my host.

```bash
# Install NGINX
sudo apt-get update
sudo apt install nginx
# Configure the firewall for SSL
sudo ufw allow 'Nginx HTTPS'
# Disable the default website
sudo rm /etc/nginx/sites-enabled/default
# Create the SSL folder and move the certificates in
sudo mkdir -p /etc/nginx/ssl
sudo chmod 600 /etc/nginx/ssl
sudo cp ~/cmbu.local.crt.pem /etc/nginx/ssl/
sudo cp ~/cmbu.local.kry.pem /etc/nginx/ssl/
```

Next I want to publish the Shared Path configured in my Docker Endpoint - this defaults to `/sharedPath` but it can be any path on your Docker host. This is where the preserved artifacts will be saved - but it's also where the logs for the pipeline execution are saved too, so I want to only expose the contents of "artifacts" folders. To do this I will use a RegEx match in the location block of my NGINX site configuration.

To publish the `/sharedPath` folder, I create a site configuration in the sites-available folder:  `/etc/nginx/sites-available/<site name>` with the configuration below - I've annotated the configuration:

```nginx
server {
        listen 443 default ssl; # Listen on port 443 using HTTPS
        server_name smcg-sc2-docker-host.cmbu.local; # My docker host's FQDN
        ssl_certificate /etc/nginx/ssl/cmbu.local.crt.pem; # SSL Certificate
        ssl_certificate_key /etc/nginx/ssl/cmbu.local.key.pem; # SSL Private Key
        location ~* /artifacts/ { # RegEx location to only allow paths with "artifacts" in the path
                root /sharedPath; # Serve files from the sharedPath (configured in the Docker Endpoint)
                rewrite ^/sharedPath(/.*)$ $1 last; # Re-write "/sharedPath/" as the artifact path includes it
        }
}
```
Next I can enable the site config, test the config and then restart NGINX to make it live:

```bash
sudo ln -s /etc/nginx/sites-available/smcg-sc2-docker-host.cmbu.local /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```
At this point I should be able to access pipeline artifacts using the artifact output path, but I should also get a `HTTP 404` for any URL that doesn't include `/artifacts/`.

To test this I've created a simple pipeline with a CI task that writes and preserves a file called "preserve.txt":

{{< img src="preserve-file.png" alt="Preserve an artifact" >}}

I've also configured an email notification to send a link to the requesting user on successful execution of the pipeline:

{{< img src="preserve-notification.png" alt="Email a link to the artifact" >}}

When the pipeline is executed, I recieve the notification:

{{< img src="preserve-email.png" alt="Email notification" >}}

And I can access the preserved file via the link:

{{< img src="preserve-download.png" alt="Downloading the preserved file" >}}
