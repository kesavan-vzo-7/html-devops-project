# HTML DevOps CI/CD Project

A local DevOps learning project using GitHub, Jenkins, Docker,
Prometheus, cAdvisor and Grafana.

## Architecture

1. Develop the animated website using HTML, CSS and JavaScript.
2. Push changes to GitHub.
3. GitHub webhook triggers Jenkins.
4. Jenkins checks out and validates the source code.
5. Jenkins builds a Docker image.
6. Jenkins deploys the website through Nginx.
7. Prometheus collects Docker container metrics through cAdvisor.
8. Grafana visualizes the collected metrics.

## Local URLs

- Website: http://localhost:8081
- Jenkins: http://localhost:8080
- Prometheus targets: http://localhost:9090/targets
- Grafana: http://localhost:3000
- cAdvisor: http://localhost:8082

## Resume the existing services

    docker start jenkins html-devops-container prometheus grafana cadvisor

## Start the monitoring stack through Docker Compose

    cd D:\html-devops-project\monitoring
    docker compose up -d

## Stop the existing services without deleting them

    docker stop jenkins html-devops-container prometheus grafana cadvisor

## Update the website

Run from the project root:

    git add index.html
    git commit -m "Update website"
    git push

The GitHub webhook should trigger Jenkins while the ngrok
tunnel is running and its configured URL is current.

## Persistence

Keep the jenkins_home, monitoring_grafana_data and
monitoring_prometheus_data Docker volumes.

Never commit credentials, access tokens, environment secrets
or sensitive backups to a public GitHub repository.
