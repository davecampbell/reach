# pelican SSG for a website

### site:  reachcare.com

This is the result of getting pretty worn down by using wordpress for simple sites or even placeholders.  The last straw is when wordpress gets hacked and all sorts of crazy gets injected.  

I found a useful setup tutorial [here](https://alexgose.com/build-blog-pelican-docker.html) and just decided to go with it for my first go.  

There are actually a few 'phases' to the setup, which seems a bit onerous, but once you get used to it, it's not that bad.  

### Phase 1 - Initial Setup
Steps 1-6 in the above article.  
This requires a docker build and some steps to do the pelican initiaization.

### Phase 2 - making some content
Step 7.

### Phase 3 - look at it locally
Step 8.  
These are command references.  
build (or re-build) the docker image.  i'm calling my image ```reach```.
```
sudo docker build -t reach .
```
now, have pelican build the website from the content and start a local webserver to see it.  
```
sudo docker run --rm -it -p 8000:8000 -v $(pwd)/content:/website/content:ro -v $(pwd)/output:/website/output reach make devserver
```

### Phase 4 - publish the website
Step 9.  
His article publishes through github actions to github pages.  That's pretty handy, and I've done that with mkdocs.  
I have this site just sending files to a dreamhost account via ftp.  
I had to add 'lftp' as an application in my image via Dockerfile.

```
sudo docker run --rm -it -v $(pwd)/content:/website/content:ro -v $(pwd)/output:/website/output reach make publish ftp_upload
```

