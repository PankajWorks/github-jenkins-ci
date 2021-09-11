# github-jenkins-ci
Demo : using github webhooks with jenkins

## Steps to test it on local machine 
### pre-reqs
- [ngrok](https://ngrok.com/) or  [smee](https://smee.io/) : This is required to provide a pulic IP
- [jenkins](https://jenkins.io)
- A custom proxy server to forward the request to jenkins

### Steps
- create a dummy github repo similar to [this](https://github.com/PankajWorks/github-jenkins-ci) 
- start ngrok in one of the terminal. It will show the public url which needs to go in the webhooks section.
```
ngrok http 9090
ngrok will forward the request on localhost 9090
```
- start the custom proxy server you can also use [webhookproxy](https://github.com/stakater/GitWebhookProxy)

```

./GitWebhookProxy -listen=localhost:9090 -upstreamURL=http://localhost:8080 -allowedPaths=/github-webhook

```

- start jenkins on docker
```
docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11
```
- login in jenkins and create a new job.
- under `Source Code Management` choose `git` and add the current repo. 
- under branches enter */main
- under `build trigger` select `GitHub hook trigger for GITScm polling`

- create [git hooks](https://docs.github.com/en/developers/webhooks-and-events/webhooks/about-webhooks) 
- [customizing web hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)

## GitHub Pull Request Builder Plugin
- [link1](https://github.com/janinko/ghprb)
