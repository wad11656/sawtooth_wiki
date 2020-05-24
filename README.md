# Sawtooth Wiki

Though the site was made using DokuWiki, the built-in Wiki markdown was largely ignored to make room for custom Javascript and HTML. This was necessary to make the site's functionality and style conform to my vision.

## Image "Lazy Loading"
Used to resolve an **Error 503** where the server was getting overloaded from trying to render too much media upon page-load. Lazy loading makes images only appear when you scroll to their location.

### Javascript
```Javascript
<JS>
    refresh_handler = function(e) {
    var elements = document.querySelectorAll("*[data-src]");
    for (var i = 0; i < elements.length; i++) {
            var boundingClientRect = elements[i].getBoundingClientRect();
            if (elements[i].hasAttribute("data-src") && boundingClientRect.top < window.innerHeight) {
                elements[i].setAttribute("src", elements[i].getAttribute("data-src"));
                elements[i].removeAttribute("data-src");
            }
        }
    };

    window.addEventListener('scroll', refresh_handler);
    window.addEventListener('load', refresh_handler);
    window.addEventListener('resize', refresh_handler);
</JS>
```

### HTML
```HTML
<HTML><img src="" data-src="lib/exe/fetch.php?media=sawtooth:walkthroughs:overview.png" width="85" /></HTML>
```

## HTML5 Video Spoiler/Reveal Button

<img src="https://raw.githubusercontent.com/wad11656/sawtooth_wiki/master/README%20media/video_spoiler.gif" width="200">

### HTML + inline Javascript & CSS
```HTML
<html>
<button title="Click to Show/Hide Content" type="button" onclick="if(document.getElementById('spoiler6') .style.display=='none') {document.getElementById('spoiler6') .style.display=''}else{document.getElementById('spoiler6') .style.display='none'};document.getElementById('video6').src = 'lib/exe/fetch.php?media=sawtooth:walkthroughs:6_-_first_commit_speed.mp4'">Show Me!</button>
<div id="spoiler6" style="display:none">
<video id="video6" width="381" height="238" controls autoplay loop muted playsinline></video>
</div>
</html>
```
