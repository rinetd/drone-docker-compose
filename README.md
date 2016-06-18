# drone-docker-compose

Trying to get drone 0.5 to work with docker compose.  
Linux only at the moment.  

# Requirements

- docker & docker-compose
- sqlite3
- jq
- apache2-utils (for htpasswd)

## Generating a htpasswd file

For the registry ([must be Bcrypt](https://docs.docker.com/registry/configuration/#auth))

```shell
htpasswd -cbB ./registry/htpasswd username password
```

# Running it

**Add an env.sh file:**

```shell
export DRONE_GITHUB_CLIENT=YOUR_GITHUB_APP_CLIENT_KEY_HERE
export DRONE_GITHUB_SECRET=YOUR_GITHUB_APP_SECRET_KEY_HERE
export DRONE_AGENT_SECRET=INSERT_RANDOM_UNIQUE_STRING_HERE
export DRONE_USER_TOKEN=THE_TOKEN_ON_YOUR_DRONE_PROFILE
export DOCKER_REGISTRY_URL=YOUR_DOCKER_REGISTRY_URL
export DOCKER_REGISTRY_USER=YOUR_DOCKER_REGISTRY_USER
export DOCKER_REGISTRY_PASSWORD=YOUR_DOCKER_REGISTRY_PASSWORD
export DOCKER_REGISTRY_HTTP_SECRET=INSERT_RANDOM_LONG_STRONG_HERE
```

**Start drone + 1 drone agent:**

```shell
./up.sh
```

**Trigger a build:**

Increments a build number and pushes to github.

```shell
./trigger_build.sh
```
