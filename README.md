# n8n-workflows

## Goal

Goal of repo is to save automation work in case docker container is deleted by accident or I have to change computers.

Make sure you sanitize all json files of credentials - they're internal ids, not direct api keys, but still good practice.

### Set up

Instructions for adding a docker instance to local to avoid cloud subscription of n8n: https://docs.n8n.io/hosting/installation/docker/

Simple set up:

```
docker volume create n8n_data

docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

In case you delete a container you'll have to run the following command again:

```
docker run -it -d --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

After your n8n instance is running, if your volume is blank you'll have to:

1. Create each workflow in the app
2. Drag and drop your json files
3. Create the required credentials (Gmail, Sheets ...etc) and run each workflow to hook them up.
