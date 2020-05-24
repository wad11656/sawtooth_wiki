# Sawtooth Wiki

Though the site was made using DokuWiki, the built-in Wiki markdown was largely ignored in favor of custom Javascript and HTML. This was necessary to make the site's functionality and style conform to my vision.

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

## Video Spoiler/Reveal Button

<img src="https://raw.githubusercontent.com/wad11656/sawtooth_wiki/master/README%20media/video_spoiler.gif" width="470">

### HTML + inline Javascript & CSS
```HTML
<html>
<button title="Click to Show/Hide Content" type="button" onclick="if(document.getElementById('spoiler6') .style.display=='none') {document.getElementById('spoiler6') .style.display=''}else{document.getElementById('spoiler6') .style.display='none'};document.getElementById('video6').src = 'lib/exe/fetch.php?media=sawtooth:walkthroughs:6_-_first_commit_speed.mp4'">Show Me!</button>
<div id="spoiler6" style="display:none">
<video id="video6" width="381" height="238" controls autoplay loop muted playsinline></video>
</div>
</html>
```

## Interactive Animated Employee Descriptions

<img src="https://raw.githubusercontent.com/wad11656/sawtooth_wiki/master/README%20media/video_spoiler.gif" width="470">

### Javascript
```Javascript
<JS>
    function changeContent(description) {
        console.log(description);
        var MyDesc = document.getElementById(description);
        document.getElementById('content').innerHTML = MyDesc.value;
    }
</JS>
```

### CSS
```CSS
<CSS>
/* General formatting */
p {
	margin: 0 0 0;
}
ul {
	margin: 0 0 0;
}
ol {
	margin: 0 0 0;
}

/* Blue box */
.container {
	display: flex;
	align-items: center;
	justify-content: initial;
}
.rectangle {
	min-height: 300px;
	height: auto;
	width: 100%;
	border-style: solid;
	border-radius: 10px 25px;
	border-width: 1px;
	border-color: #00008b;
	background-color: #add8e6;
	transition: all .5s linear;
}
.boxcont {
	color: darkblue;
}

/* Striped UL */
ul.striped-list {
	list-style-type: none;
	margin: 0;
	padding: 0;
	max-width: 200px;
}
ul.striped-list>li {
	border-bottom: 1px solid rgb(221, 221, 221);
	padding: 6px;
}
ul.striped-list>li:nth-of-type(odd) {
	background-color: #e9e9f9;
}
ul.striped-list>li:last-child {
	border-bottom: none;
}

/* Class for placeholder text */
.tab {
	position: absolute;
	left: 36%;
	color: darkblue;
}

/* Growing employee images */
img,
span {
	display: table-cell;
}
.grow {
	transition: all .2s ease-in-out;
}
.grow:hover {
	transform: scale(1.1);
}

/* Main background image */
#main {
	width: 100%;
}
#photo {
	display: flex;
}
#photo>#photo-center {
	width: 100%;
	position: relative;
	display: block;
	margin-left: auto;
	margin-right: 0px;
}
#large {
	width: 100%;
}

/* Server Ops 2 - Bob */
#ops2 {
	width: 17%;
	position: absolute;
	left: 44%;
	right: 0px;
	top: 0%;
	z-index: 1;
}

/* Server Ops 1 - Alice */
#ops1 {
	width: 17%;
	position: absolute;
	left: 85%;
	right: 0px;
	top: 0%;
	z-index: 1;
}

/* QA Black Box - Steve */
#qablack {
	width: 10%;
	position: absolute;
	left: 60%;
	right: 0px;
	top: 36%;
	z-index: 1;
}

/* QA Load Testing - Jerry */
#qaload {
	width: 20%;
	position: absolute;
	left: 63%;
	right: 0px;
	top: 65%;
	z-index: 1;
}

/* QA Software Engineer - Charlie */
#qasoft {
	width: 17%;
	position: absolute;
	left: 73%;
	right: 0px;
	top: 38%;
	z-index: 1;
}

/* Manager 2 - Peter */
#mang2 {
	width: 15%;
	position: absolute;
	left: 22%;
	right: 0px;
	top: -6%;
	z-index: 1;
}

/* Manager 1 - Craig */
#mang1 {
	width: 13%;
	position: absolute;
	left: 6%;
	right: 0px;
	top: -4%;
	z-index: 1;
}

/* Developer 1 - Bill */
#soft1 {
	width: 15%;
	position: absolute;
	left: 0%;
	top: 48.5%;
	z-index: 1;
}

/* Developer 2 - Jared */
#soft2 {
	width: 9%;
	position: absolute;
	left: 3%;
	right: 0px;
	top: 22%;
	z-index: 1;
}
</CSS>
```

### HTML
```HTML
<html>
<a name="top_header"></a><br>
<strong><div style="font-size:20px" class="rectangle container" id="content"><span class="tab">Hover over a character to discover their Workflow Woes!<br><br><br><br><br></span>
</div></strong>
<br />
<br />
<br />
<div id="main">
        <div id="photo">
           <div id="photo-center">   
             <img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:traditional3.jpg" id="large">

                <a onmouseover="changeContent('desc1')" href="#top_header"><img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:server_ops2.png" id="ops2" class="grow"></a>
                <input type="hidden" id="desc1" value="&lt;span class=&quot;boxcont&quot;&gt;&lt;strong&gt;&lt;p style=&quot;padding-left:10px; text-decoration: underline;&quot; &gt;Server Op 2 - &lt;style=&quot;text-decoration:none !important&quot;&gt;Bob&lt;/style&gt;&lt;img src=&quot;https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:server_ops2.png&quot; style=&quot;display: inline-block&quot; width=&quot;13%&quot;&gt;&lt;/p&gt;&lt;/strong&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt; &lt;/p&gt;&lt;div style=&quot;background-color:#e8f4f8;&quot;&gt;&lt;p style=&quot;color:#000;&quot;&gt;&lt;strong&gt;Primary Needs:&lt;/strong&gt;&lt;br&gt;&lt;ol&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Stop server crashes caused by huge deploys&lt;/li&gt;&lt;li style=&quot;color:#000;&quot;&gt;Consistent &amp;amp; reliable code deploys&lt;/li&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Ability to roll back infrastructure&lt;/li&gt;&lt;/ol&gt;&lt;/p&gt;&lt;/div&gt;&lt;br&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt;Server Operations Engineer 2 has been pulling off the heroic efforts for buggy deploys that cause problems for customers. He is tired of seeing deploys break things, so he would love to see deploys occur reliably, consistently, and affect fewer customers if problems do sneak through. He would love to be able to roll back infrastructure to a stable point if needed.&lt;/p&gt;&lt;/span&gt;">
                 
                <a onmouseover="changeContent('desc2')" href="#top_header"><img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:server_ops1.png" id="ops1" class="grow"></a>
                ​<input type="​hidden"​ id="desc2" value="&lt;span class=&quot;boxcont&quot;&gt;&lt;strong&gt;&lt;p style=&quot;padding-left:10px; text-decoration: underline;&quot; &gt;Server Op 1 - &lt;style=&quot;text-decoration:none !important&quot;&gt;Alice&lt;/style&gt;&lt;img src=&quot;https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:server_ops1.png&quot; style=&quot;display: inline-block&quot; width=&quot;13%&quot;&gt;&lt;/p&gt;&lt;/strong&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt; &lt;/p&gt;&lt;div style=&quot;background-color:#e8f4f8;&quot;&gt;&lt;p style=&quot;color:#000;&quot;&gt;&lt;strong&gt;Primary Needs:&lt;/strong&gt;&lt;br&gt;&lt;ol&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Provide reliable simultaneous testing environments in high quantity&lt;/li&gt;&lt;li style=&quot;color:#000;&quot;&gt;Provide readily available, highly accessible VMs&lt;/li&gt;&lt;/ol&gt;&lt;/p&gt;&lt;/div&gt;&lt;br&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt;Server Operations Engineer 1 is swamped with repeated demands to build VMs for developers and testers to use. She is to the point where she would rather just build a bunch of servers and leave them up for her coworkers to test on, so she has done just that. Doing so is expensive and eventually configurations and settings on those servers drift apart from the production systems. She would love to be able to provide consistent testing environments that mirror production on demand.&lt;/p&gt;&lt;/span&gt;​">
                  
                <a onmouseover="changeContent('desc3')" href="#top_header"><img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:soft_engineer1.png" id="soft1" class="grow"></a>
                <input type="hidden" id="desc3" value="&lt;span class=&quot;boxcont&quot;&gt;&lt;strong&gt;&lt;p style=&quot;padding-left:10px; text-decoration: underline;&quot; &gt;Developer 1 - &lt;style=&quot;text-decoration:none !important&quot;&gt;Bill&lt;/style&gt;&lt;img src=&quot;https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:soft_engineer1.png&quot; style=&quot;display: inline-block&quot; width=&quot;11%&quot;&gt;&lt;/p&gt;&lt;/strong&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt; &lt;/p&gt;&lt;div style=&quot;background-color:#e8f4f8;&quot;&gt;&lt;p style=&quot;color:#000;&quot;&gt;&lt;strong&gt;Primary Needs:&lt;/strong&gt;&lt;br&gt;&lt;ol&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Eliminate long lines of devs waiting for an available server to run their code&lt;/li&gt;&lt;li style=&quot;color:#000;&quot;&gt;Pull requests on master branch &amp; feature branches trigger builds automatically&lt;/li&gt;&lt;/ol&gt;&lt;/p&gt;&lt;/div&gt;&lt;br&gt&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt;Developer 1 is tired of waiting in the queue for building his code on the build server. He feels less productive than he knows he can be because there are several other teams competing for the same resources. The worst part is how he has to go down to the physical build server and see how inconsistent the line can be, sometimes he only has to wait minutes to get a spot, sometimes it is hours or days before he can get a slot. He would love to see his pull requests on the development and feature branches of his project trigger builds on a server that he does not have to physically stand in line for.&lt;/p&gt;&lt;/span&gt;">
                
                <a onmouseover="changeContent('desc4')" href="#top_header"><img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:soft_engineer2.png" id="soft2" class="grow"></a>
                <input type="hidden" id="desc4" value="&lt;span class=&quot;boxcont&quot;&gt;&lt;strong&gt;&lt;p style=&quot;padding-left:10px; text-decoration: underline;&quot; &gt;Developer 2 - &lt;style=&quot;text-decoration:none !important&quot;&gt;Jared&lt;/style&gt;&lt;img src=&quot;https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:soft_engineer2.png&quot; style=&quot;display: inline-block&quot; width=&quot;6%&quot;&gt;&lt;/p&gt;&lt;/strong&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt; &lt;/p&gt;&lt;div style=&quot;background-color:#e8f4f8;&quot;&gt;&lt;p style=&quot;color:#000;&quot;&gt;&lt;strong&gt;Primary Needs:&lt;/strong&gt;&lt;br&gt;&lt;ol&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Stop having to spin up a VM on local PC after each code change to run tests&lt;/li&gt;&lt;li style=&quot;color:#000;&quot;&gt;Code is auto-tested without needing to manually configure VM settings&lt;/li&gt;&lt;/ol&gt;&lt;/p&gt;&lt;/div&gt;&lt;br&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt;Developer 2 is committed to writing unit tests for every aspect of his code, but it is very tedious for him to set up and tear down VMs on his local machine just to verify that each change he makes to the code base passes each unit test. &lt;br&gt;He would love to see unit testing happen after his builds are ready ideally without having to worry about settings on VMs.&lt;/p&gt;&lt;/span&gt;">
                
                <a onmouseover="changeContent('desc5')" href="#top_header"><img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:qa_black_box.png" id="qablack" class="grow"></a>
                <input type="hidden" id="desc5" value="&lt;span class=&quot;boxcont&quot;&gt;&lt;strong&gt;&lt;p style=&quot;padding-left:10px; text-decoration: underline;&quot; &gt;Black Box Tester - &lt;style=&quot;text-decoration:none !important&quot;&gt;Steve&lt;/style&gt;&lt;img src=&quot;https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:qa_black_box.png&quot; style=&quot;display: inline-block&quot; width=&quot;8%&quot;&gt;&lt;/p&gt;&lt;/strong&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt; &lt;/p&gt;&lt;div style=&quot;background-color:#e8f4f8;&quot;&gt;&lt;p style=&quot;color:#000;&quot;&gt;&lt;strong&gt;Primary Needs:&lt;/strong&gt;&lt;br&gt;&lt;ol&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Be notified immediately when builds are ready for black box testing&lt;/li&gt;&lt;li style=&quot;color:#000;&quot;&gt;Quickly attach test results to respective build and send back to associated devs to fix&lt;/li&gt;&lt;/ol&gt;&lt;/p&gt;&lt;/div&gt;&lt;br&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt;Black Box Tester fiddles around a lot with features and products trying to break things. Some days, it seems like he has a lot of time on his hands--he just waits for someone to give him something to test, and other days, he does not have enough time to even go through the full testing checklist for anything. Either way, it seems like all the product managers are clamoring for more quality control measures and he is just caught in the middle. &lt;br&gt;He would love to know when new items are ready for him to test. Once he finds an issue, he would love to quickly connect his reports with the respective build so he can send his feedback back to those responsible for replicating and for fixing the problems&lt;/p&gt;&lt;/span&gt;">
                
                <a onmouseover="changeContent('desc6')" href="#top_header"><img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:qa_load_group.png" id="qaload" class="grow"></a>
                <input type="hidden" id="desc6" value="&lt;span class=&quot;boxcont&quot;&gt;&lt;strong&gt;&lt;p style=&quot;padding-left:10px; text-decoration: underline;&quot; &gt;Load Testers - &lt;style=&quot;text-decoration:none !important&quot;&gt;Server Ops / Dev-Testers&lt;/style&gt;&lt;img src=&quot;https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:qa_load_group.png&quot; style=&quot;display: inline-block&quot; width=&quot;13%&quot;&gt;&lt;/p&gt;&lt;/strong&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt; &lt;/p&gt;&lt;div style=&quot;background-color:#e8f4f8;&quot;&gt;&lt;p style=&quot;color:#000;&quot;&gt;&lt;strong&gt;Primary Needs:&lt;/strong&gt;&lt;br&gt;&lt;ol&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Automated infrastructure provisioning and auto-configuration of load testing tools&lt;/li&gt;&lt;li style=&quot;color:#000;&quot;&gt;Make load testing optional per build/deploy in CI/CD pipeline&lt;/li&gt;&lt;/ol&gt;&lt;/p&gt;&lt;/div&gt;&lt;br&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt;Load testing is a joint effort between Server Ops Engineers and Dev-Testers. Really whoever is available to do it does it and it usually involves manually setting up a bunch of VMs that run code that generates lots of web requests. They would love to see load testing that uses automated infrastructure provisioning and tools to execute load testing. They would love to see this be an option in the testing and release pipeline because not every build/deploy needs to be tested under load.&lt;/p&gt;&lt;/span&gt;">
                
                <a onmouseover="changeContent('desc7')" href="#top_header"><img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:qa_soft_engineer.png" id="qasoft"  class="grow"></a>
                <input type="hidden" id="desc7" value="&lt;span class=&quot;boxcont&quot;&gt;&lt;strong&gt;&lt;p style=&quot;padding-left:10px; text-decoration: underline;&quot; &gt;Developer-Tester - &lt;style=&quot;text-decoration:none !important&quot;&gt;Charlie&lt;/style&gt;&lt;img src=&quot;https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:qa_soft_engineer.png&quot; style=&quot;display: inline-block&quot; width=&quot;13%&quot;&gt;&lt;/p&gt;&lt;/strong&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt; &lt;/p&gt;&lt;div style=&quot;background-color:#e8f4f8;&quot;&gt;&lt;p style=&quot;color:#000;&quot;&gt;&lt;strong&gt;Primary Needs:&lt;/strong&gt;&lt;br&gt;&lt;ol&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Stop having to wait for Server Ops employees to set up correct environments each test&lt;/li&gt;&lt;li style=&quot;color:#000;&quot;&gt;Get test results back to devs ASAP while the code is still fresh in their minds&lt;/li&gt;&lt;/ol&gt;&lt;/p&gt;&lt;/div&gt;&lt;br&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt;Developer-Tester develops the testing frameworks that run regression tests on various products. His work ensures that new features don't break existing features. Running lots of different regression tests is a lot for him to handle because some jobs can take several hours and he often has to wait on Server Operations for a proper environment to be fully configured. He would love to keep up with the demand for running the tests on different web browsers as well. Several product managers have expressed concern that his test results and feedback aren't getting back to the developers quick enough--by the time the environment is set up and the tests are run, the developers are working on new features and it's hard for them to remember what was tested.&lt;/p&gt;&lt;/span&gt;">
                
                <a onmouseover="changeContent('desc8')" href="#top_header"><img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:manager1.png" id="mang1" class="grow"></a>
                <input type="hidden" id="desc8" value="&lt;span class=&quot;boxcont&quot;&gt;&lt;strong&gt;&lt;p style=&quot;padding-left:10px; text-decoration: underline;&quot; &gt;Manager 1 - &lt;style=&quot;text-decoration:none !important&quot;&gt;Craig&lt;/style&gt;&lt;img src=&quot;https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:manager1.png&quot; style=&quot;display: inline-block&quot; width=&quot;8%&quot;&gt;&lt;/p&gt;&lt;/strong&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt; &lt;/p&gt;&lt;div style=&quot;background-color:#e8f4f8;&quot;&gt;&lt;p style=&quot;color:#000;&quot;&gt;&lt;strong&gt;Primary Needs:&lt;/strong&gt;&lt;br&gt;&lt;ol&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Improvement over current dev processes (i.e., efficiency, accuracy)&lt;/li&gt;&lt;li style=&quot;color:#000;&quot;&gt;Consistent deployment procedures across the company&lt;/li&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Proof of the usefulness and reliability of CI/CD pipeline tests&lt;/li&gt;&lt;/ol&gt;&lt;/p&gt;&lt;/div&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt;&lt;br&gt;Manager 1 supervises several teams and products. No longer directly in development, it is important for him to see improvement in processes that his teams follow. A major responsibility is to ensure that all proper procedures have been followed before a production deploy can occur. He trusts his teams to thoroughly review and test their work as well as they can, but he is not confident yet in automated testing to deploy to production without his explicit approval. He believes they are almost there, but he wants to manually approve kicking off whatever actions move new code into production.&lt;/p&gt;&lt;/span&gt;"></a>
                
                <a onmouseover="changeContent('desc9')" href="#top_header"><img src="https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:manager2.png" id="mang2"  class="grow"></a>
                <input type="hidden" id="desc9" value="&lt;span class=&quot;boxcont&quot;&gt;&lt;strong&gt;&lt;p style=&quot;padding-left:10px; text-decoration: underline;&quot; &gt;Manager 2 - &lt;style=&quot;text-decoration:none !important&quot;&gt;Peter&lt;/style&gt;&lt;img src=&quot;https://sawtoothcapstone.com/lib/exe/fetch.php?media=sawtooth:deliverables:manager2.png&quot; style=&quot;display: inline-block&quot; width=&quot;8%&quot;&gt;&lt;/p&gt;&lt;/strong&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt; &lt;/p&gt;&lt;div style=&quot;background-color:#e8f4f8;&quot;&gt;&lt;p style=&quot;color:#000;&quot;&gt;&lt;strong&gt;Primary Needs:&lt;/strong&gt;&lt;br&gt;&lt;ol&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Consistently integrate new tech and adopt new work models&lt;/li&gt;&lt;li style=&quot;color:#000;&quot;&gt;Understand how to use CI/CD containerization (i.e., Kubernetes, Docker)&lt;/li&gt;&lt;li style=&quot;color:darkblue;&quot;&gt;Understand the usefulness &amp; security of CI/CD containers&lt;/li&gt;&lt;/ol&gt;&lt;/p&gt;&lt;/div&gt;&lt;p style=&quot;padding-left:10px; font-size:14px;&quot;&gt;Manager 2 is concerned that important new technologies and models are passing the development and operations teams by, restricting future growth and allowing competitors to capitalize on new market sectors with more flexibility and agility than his teams can currently provide. He really wants to understand containerization technologies without having to dive in and actually do it himself: How Kubernetes/Docker work; what needs to be done to smoothly deploy and manage applications on container based infrastructure; what do different cloud service providers offer for containerization technologies and what pros and cons exist; how can containerization enable and empower development, testing, and operational process improvements; how secure containers/cloud container services are; how deployment pipelines interact with those services, etc.&lt;/p&gt;&lt;/span&gt;">
          </div>
        </div> 
      </div>
</html>
```
