Ansible Role: Hoarder-docker
============================

Install Hoarder Docker Compose project.

- https://hoarder.app/
- https://github.com/hoarder-app/hoarder

Requirements
------------

Requires the following to be installed:
- docker
- docker compose

Role Variables
--------------

Common Docker projects variables:

```yaml
# Base directory for Docker projects
docker_projects_path: # /var/apps
```

Available role variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker project variables

hoarder_project_name: hoarder

# Docker project dynamic vars (uses `docker_project_name` prefix, adapt if overridden)

hoarder_traefik_loadbalancer_server_port: 3000

# Main service additional docker-compose options (ex: cpu_shares, deploy, ...)
hoarder_compose_service_additional_options: |
  #ports:
  #  - 3000:3000
```

```yaml
# Hoarder project variables

# ghcr.io/hoarder-app/hoarder image version
hoarder_docker_version: release

# gcr.io/zenika-hub/alpine-chrome image version
hoarder_chrome_version: 123

# getmeili/meilisearch image version
hoarder_meilisearch_version: v1.11.1
```

```yaml
# Public address of service
hoarder_nextauth_url: http://localhost:3000

# Random string used to sign the JWT tokens. Generate one with `openssl rand -base64 36`
hoarder_nextauth_secret: super_random_string
# Master key configured for meilisearch
hoarder_meili_master_key: another_random_string

# Sets the maximum allowed asset size (in MB) to be uploaded
hoarder_max_asset_size_mb: 4
# If set to true, latest release check will be disabled in the admin panel.
hoarder_disable_new_release_check: false
```

```yaml
# Authentication / Signup

# If enabled, no new signups will be allowed and the signup button will be disabled in the UI
hoarder_disable_signups: false
# If enabled, only signups and logins using OAuth are allowed and the signup button and login form for local accounts will be disabled in the UI
hoarder_disable_password_auth: false
# The "wellknown Url" for openid-configuration as provided by the OAuth provider
hoarder_oauth_wellknown_url:
# The "Client Secret" as provided by the OAuth provider
hoarder_oauth_client_secret:
# The "Client ID" as provided by the OAuth provider
hoarder_oauth_client_id:
# Full list of scopes to request (space delimited)
hoarder_oauth_scope: "openid email profile"
# The name of your provider. Will be shown on the signup page as "Sign in with <name>"
hoarder_oauth_provider_name: "Custom Provider"
# Whether existing accounts in hoarder stored in the database should automatically be linked with your OAuth account. Only enable it if you trust the OAuth provider!
hoarder_oauth_allow_dangerous_email_account_linking: false
```

```yaml
# Inference Configs (For automatic tagging)
hoarder_openai_api_key:
hoarder_openai_base_url:
hoarder_ollama_base_url:
hoarder_ollama_keep_alive:
hoarder_inference_text_model: gpt-4o-mini
hoarder_inference_image_model: gpt-4o-mini
hoarder_inference_context_length: 2048
hoarder_inference_lang: english
hoarder_inference_job_timeout_sec: 30
```

```yaml
# Crawler Configs
hoarder_crawler_num_workers: 1
hoarder_browser_web_url:
hoarder_browser_websocket_url:
hoarder_browser_connect_ondemand: false
hoarder_crawler_download_banner_image: true
hoarder_crawler_store_screenshot: true
hoarder_crawler_full_page_screenshot: false
hoarder_crawler_full_page_archive: false
hoarder_crawler_job_timeout_sec: 60
hoarder_crawler_navigate_timeout_sec: 30
hoarder_crawler_video_download: false
hoarder_crawler_video_download_max_size: 50
hoarder_crawler_video_download_timeout_sec: 600
```

```yaml
# OCR Configs
hoarder_ocr_cache_dir: /tmp
hoarder_ocr_langs: eng
hoarder_ocr_confidence_threshold: 50
```

Dependencies
------------

This role depends on :
- [djuuu.docker_project](https://github.com/Djuuu/ansible-role-docker-project)

Some variables allow integration with:
- [djuuu.traefik_docker](https://github.com/Djuuu/ansible-role-traefik-docker)

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: false

  roles:
    - djuuu.hoarder_docker
```

License
-------

Beerware License
