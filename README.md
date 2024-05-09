<h1>Burp Suite | A Security Testing Tool In Web Application Security</h1>

<h2>Description</h2>
<p>Here, I'll explore the basics of the web application security testing tool, Burp Suite, as well as its core features and options, paired with demonstrations. I’ve learned much more about web application vulnerabilities through the practical approach with this tool. This tool is very useful, and I plan to invest more time in it to increase my technical skills.</p>
<br />
<h2>Utilities Used</h2>

- <b>Burp Suite Community Edition</b>
- <b>Browser (e.g., Google Chrome and Firefox)</b>
<h2>Environments Used</h2>

- <b>VMware Hypervisor </b>
- <b>Kali Linux Virtual Machine (VM)</b>
- <b>Metasploitable 2 (Vulnerable VM)</b>

<h2>Lab Walk-through:</h2>
<p>This short demonstration will examine a popular security testing tool, Burp Suite, that is frequently used in web application security testing. The report will review the methods to install and use the tool. Then the tools’ features will be described with sample scenarios.</p>
<br />
<h3>Burp Suite</h3>
Also referred as Burp, Burp Suite is a framework composed of a set of tools used for penetration testing web applications. It does this by essentially capturing the network traffic between the client (or attacker) and a web server and manipulating that traffic. Burp Suite is available in different editions. For this report, I will be focusing on reviewing Burp Suite Community Edition and its features, which is open-source and free to use within legal boundaries.
<br/>
<h3>Installation</h3>
Burp Suite is available to download on Linux distributions and Windows operating systems. Each provided with their respective installers for Burp Suite Community and Burp Suite Professional on the Burp Suite downloads page. Burp Suite already comes pre-installed on a Kali Linux VM, but if it’s missing on your Kali installation, you can update your machine via <b>sudo apt update</b> and then easily install it from the Kali Linux apt repositories.
<br/>
<h3>Exploring Burp Suite</h3>
Now, let’s launch the application. At first stage of boot, you will be prompted to choose a type of project to start on, I will start with a “Temporary Project” for the entirety of this report. Once the project loads up, you are met with the dashboard – providing a coupe of functions such as defining background tasks and an event log that displays information about the actions performed by Burp Suite (e.g., starting the proxy and network connection details). 
<br />
<h3>Proxy</h3>
Burp Suite’s Proxy feature is a crucial tool within the Java-based framework – enabling the capture of requests and responses between a user and the target web server. This intercepted traffic can be manipulated, sent to other features within Burp Suite for further processing, or allowed to continue to its destination. This ability to intercept web traffic is what makes Burp Suite an invaluable tool for testing web applications.
<h4>Foxy Proxy</h4>
Before I proceed, I would like to mention the browser extension for Burp Suite’s Proxy function, FoxyProxy. I recommend this extension so that it is easy to swap between configurations. It makes the process to configure local web browser traffic to redirect traffic through Burp Suite much easier. I am using Firefox to configure FoxyProxy, but it should be a similar process for other browsers. First, I will install the FoxyProxy Basic extension. Once it’s installed, I click the Extensions button that appears at the top right of my browser window. Then, I click on the FoxyProxy button to access the FoxyProxy options pop-up window.
<br />
<img src="https://i.imgur.com/f1HBOQE.png" height="45%" width="45%" alt="Foxy Proxy > Options"/>
<br />
In that pop-up window, we'll click the <b>Options</b> button--opening a new browser tab with FoxyProxy configurations. Next, click the <b>Add</b> button under the Proxies tab to create a new proxy configuration.
<img src="https://i.imgur.com/MxTr0RT.png" height="80%" width="80%" alt="Add Button"/>
<br />
Add these details in the following fields:

- <b>Title</b>: Burp (or your preference)
- <b>Proxy IP</b>: 127.0.0.1
- <b>Port</b>: 8080

Now, click the <b>Save</b> button to save the configurations made and then click on the FoxyProxy icon once again at the top right of the Firefox browser and select the 'Burp' configuration. Now, the browser traffic will be redirected through <b>127.0.0.1:8080</b>.
<br/>
<img src="https://i.imgur.com/b3RrAEZ.png" height="40%" width="40%" alt="Burp Configuration Created"/>
<br />
To test the proxy, I will navigate back to Burp Suite and make sure that the <b>Intercept</b> feature is turned on in the <b>Proxy</b> tab. I go back to Firefox and travel to any webpage. A request should be intercepted by Burp Suite, as shown below.
<br />
<img src="https://i.imgur.com/xN0qwoe.png" height="60%" width="60%" alt="Intercept is on"/>
<br />
<img src="https://i.imgur.com/4wAucN3.png" height="90%" width="90%" alt="Intercepted GET Request"/>
<br />
<h4>Intercept</h4>
Now is the perfect time to take a closer look at the Intercept tab – which is the main functionality of Burp Suite’s Proxy tool. It sits between us (the users) and whatever website we’re communicating with and allows us to forward requests, drop requests, or take some action on them. In this case it seems I’ve intercepted a GET request to the PortSwigger homepage for Burp Suite. Here, I can use the Intercept tool to send off something different than what we have here. I can try sending a POST request instead of a GET request, so I’ll modify it by simply changing ‘GET’ at the top of the request to ‘POST’. Now, I'll hit <b>Forward</b> to send it off and that will forward the request to the browser. Back on the browser, this error message will display because a GET request wasn't sent to it, but this shows how the proxy can function.
<br/>
<img src="https://i.imgur.com/7lw4Z4F.png" height="60%" width="60%" alt="GET changed to POST"/>
<br />
<img src="https://i.imgur.com/WkZAXx0.png" height="60%" width="60%" alt="Error page on browser"/>
<br />
You wouldn’t want to do this process all the time for every single website you visit. Rather than intercepting every request, you might as well have the intercept turned off and analyze recent requests through the <b>HTTP history</b> tab.
<br/>
<img src="https://i.imgur.com/J7nXdps.png" height="80%" width="80%" alt="HTTP history tab"/>
<br />
On the HTTP history tab, you have your HTTP requests on the left and the server responses on the right for a more in-depth look. Here, you can filter through which type of content you want to see. You may want to only look at images or filter the results by response code. I can also filter by scope. Say you only want to view certain traffic, just the traffic from our targeted web application. We can do this by adding it to scope. 
<br/>
<h3>Scope</h3>
One of the most important aspects of using Burp Suite is Scoping. Capturing and logging all this traffic can quickly become overwhelming and inconvenient, especially when you would only want to focus on specific web applications. This is where the Scope function comes in handy. Setting a scope for the project will define what gets proxied and logged in Burp Suite. We can restrict Burp Suite to target only the specific web application(s) considered for testing. We can do this by switching to the <b>Target</b> tab, right-clicking on the target from the list on the left-hand panel and selecting <b>Add to Scope</b>. Then we'll be prompted to choose whether we want to stop logging anything that is not in scope, and in most cases, that would be <b>yes</b>. Here, I have added the IP address of the vulnerable VM, Metasploitable 2 (MS2), containing its Damn Vulnerable Web Application (DVWA) server.
<br />
<img src="https://i.imgur.com/fehyJRL.png" height="60%" width="60%" alt="Add to scope"/>
<br />
<img src="https://i.imgur.com/6ob0Dht.png" height="60%" width="60%" alt="Yes..."/>
<br />
To check the scope, we can switch to the Scope settings sub-tab within the <b>Target</b> -- the window allows us to control the target scope by including or excluding domains or IP addresses.
<br/>
<img src="https://i.imgur.com/1Q85GqD.png" height="60%" width="60%" alt="Target scope"/>
<br />
However, the HTTP history sub-tab under Proxy can still display unwanted traffic, that's because we must adjust the filter to <b>Show only in-scope items</b>.
<br />
<img src="https://i.imgur.com/fWY2FYU.png" height="60%" width="60%" alt="Configure filter"/>
<br />
<h3>Repeater</h3>
This well-known function allows for capturing, modifying, and resending the same request multiple times. This feature is particularly useful when crafting payloads through trial and error (e.g., SQL injections) or testing for endpoint vulnerabilities. Here, on the HTTP history sub-tab under Proxy, I can right-click on a failed attempt to log in to the <b>Brute Force</b> page of the DVWA server and click <b>Send to Repeater</b>.
<br/>
<img src="https://i.imgur.com/3ppkf09.png" height="85%" width="85%" alt="GET request of failed login attempt"/>
<br />
Once it is sent to Repeater, you can navigate to the Repeater tab, and it will have that request there for modification. We can modify some values (e.g., username and password parameters) and send the new request as many as one would prefer.
<br />
<img src="https://i.imgur.com/iXkqetF.png" height="85%" width="85%" alt="Send to Repeater"/>
<br />
The credentials that DVWA gives you to log in are <b>admin:password</b>. So, from the failed request, we can assign the username and password variable values to <b>admin:password</b>. The previous failed to attempt to login came with a response detailing that the "Username and/or password" was incorrect. Let's see what happens when we use Repeater to send a modified request with the correct credentials.
<br />
<img src="https://i.imgur.com/TCpytCy.png" height="85%" width="85%" alt="HTTP Response of Successful Login"/>
<br />
As you can see, we get a clearly different result from this modified request. Looking at the <b>Response</b> section in the screenshot above, we have successfully logged in with valid credentials.
<br />
<img src="https://i.imgur.com/TsMB8Uk.png" height="50%" width="50%" alt="Welcome to the password protected area..."/>
<br />
This process can take some manual work to perform; the Intruder feature can add some automation.
<br />
<h3>Intruder</h3>
This feature has much more available in the professional version of Burp Suite, but it allows for spraying target endpoints with requests, this is commonly used for brute-force attacks or fuzzing endpoints. Now I’ll use the same request I sent to the Repeater earlier to execute something closer to a brute-force attack. I will again fail to login into the Login Page under the Brute Force vulnerability section on the DVWA server and send that request to the <b>Intruder</b> feature this time.
<br />
<img src="https://i.imgur.com/uz98KSH.png" height="60%" width="60%" alt="Send to Intruder"/>
<br />
<img src="https://i.imgur.com/BzvQksN.png" height="85%" width="85%" alt="Payload Position and Attack Type"/>
<br />
The values highlighted in green are the positions where the payload will be administered. In the <b>Choose an attack type </b> section, I will change the <b>Attack type</b> from 'Sniper' to 'Cluster bomb'. I choose this for a more effective brute-force attack. In a brute-force attack, you'd usually attempt to insert some word lists of usernames and passwords to see what will gain access. Ideally, you would like each username in one wordlist to pair with each password in another all within one payload. We can configure this process in the <b>Payload</b> sub-tab. There are two payload sets I can define -- where <b>Payload set 1</b> will insert the payload for the first payload position (users), and <b>Payload set 2</b> will insert the payload for the second payload (passwords).
<br />
<img src="https://i.imgur.com/S5j1A6p.png" height="80%" width="80%" alt="Payload sets 1 and 2"/>
<br />
For both Payload sets 1 and 2, I’ll upload a very simple wordlist of potential strings (composed of usernames or passwords) that could be used as a payload against the web application. There is also a setting where you can utilize a grep function included to flag resulting items that would indicate a certain condition. For example, I can add the following expression to flag a result that would indicate a successful login from the attack.
<br />
<img src="https://i.imgur.com/jtORW7D.png" height="60%" width="60%" alt="Grep - Match"/>
<br />
Once the payload is configured, we can click the <b>'Start Attack'</b> button. Once it's finished it looks like I have received one response with a successful login!
<br />
<img src="https://i.imgur.com/18SMVm6.png" height="85%" width="85%" alt="Successful Attack!"/>
<br />
<h2>Helpful References</h2>

- [Burp Suite: The basics](https://tryhackme.com/r/room/burpsuitebasics)
- [Testing Tools Resource](https://owasp.org/www-project-web-security-testing-guide/stable/6-Appendix/A-Testing_Tools_Resource)
