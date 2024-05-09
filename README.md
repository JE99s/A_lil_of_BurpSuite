# A_lil_of_BurpSuite
<h1>Burp Suite; A Security Testing Tool In Web Application Security</h1>

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
<img src="https://i.imgur.com/f1HBOQE.png" height="80%" width="80%" alt="Foxy Proxy > Options"/>
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
<img src="https://i.imgur.com/b3RrAEZ.png" height="80%" width="80%" alt="Burp Configuration Created"/>
<br />
To test the proxy, I will navigate back to Burp Suite and make sure that the <b>Intercept</b> feature is turned on in the <b>Proxy</b> tab.
<br />
<img src="https://i.imgur.com/FlRsoJv.png" height="80%" width="80%" alt="Disable SMTP authentication"/>
<br />
<h3>Install and Configure Thunderbird Application</h3>
The email server should be ready to go and it is time to test it right now. Here, we'll be <a href="https://www.thunderbird.net/en-US/" target="_blank">installing</a> and using the open-source email client, Thunderbird.
<br/>
<img src="https://i.imgur.com/ODKzhwk.png" height="80%" width="80%" alt="Download Thunderbird Setup.exe"/>
<br />
Once it is installed, we'll configure the user accounts we created earlier during our hMailServer configurations. On the Local folders, create a new account and select <b>Email</b>. Let's make sure we choose the option to use an existing email. If a pop-up named <b>Mail Account Setup</b> appears, provide the usernames, Email addresses, and passwords we created earlier.
<br/>
<img src="https://i.imgur.com/nL24ToQ.png" height="60%" width="60%" alt="Mail Account Setup"/>
<br />
In case your configuration of Thunderbird is failing, use a manaul configuration to define the server names in the <b>IMAP</b> and <b>SMTP</b> sections. Set the server name as "localhost" for outgoing configurations. I did this for both users accounts <b>jacob@utsarr.com</b> and <b>user1@utsarr.com</b>.
<br/>
<img src="https://i.imgur.com/mUwUxSF.png" height="60%" width="60%" alt="Manual Configuration"/>
<img src="https://i.imgur.com/iR5zHwK.png" height="60%" width="60%" alt="Manual Configuration for user1"/>
<br />
Then, we should receive a warning message. Let's check the box that says, "I understand the risks", and click <b>Confirm</b> to continue.
<br/>
<img src="https://i.imgur.com/alm6uXG.png" height="60%" width="60%" alt="Warning!"/>
<br />
Then, we'll log in to user accounts we finished configuring.
<br/>
<h3>Send Yourself an E-mail</h3>
Once we have create Thunderbird profiles based from the hMailServer accounts, we'll try sending a couple of test emails to ensure communication between these accounts.
<br/>
<img src="https://i.imgur.com/Zfee9lp.png" height="75%" width="75%" alt="Tunderbird incoming email"/>
<br />
<img src="https://i.imgur.com/nfjFkSw.png" height="75%" width="75%" alt="Greetings message received"/>
<br />
