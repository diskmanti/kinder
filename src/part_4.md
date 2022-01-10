# Linux_Tweet_App

All the source code for this app is located under linux_tweet_app folder.

This app was build using podman and pushed to dockerhub:

```bash
podman build -f /linux_tweet_app/Dockerfile --tag linux_tweet_app
podman tag localhost/linux_tweet_app diskmanti/linux_tweet_app:v1
podman push diskmanti/linux_tweet_app:v1
```
