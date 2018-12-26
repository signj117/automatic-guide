
## Jenkins Remote Access API

The same Projects for WebSphere (deploy, restart, etc.) available in the Jenkins GUI can also be invoked via HTTP Post using a REST-style API.

The command below deploys WebSphere app 'MyWebApp' in the cm12345 folder to the WAS855-01UTCell.

`curl -X POST -k -u &lt;uid&gt;:&lt;yourJenkinsAPIToken&gt; <BR>&quot;https://deploy.example.com/<br>job/appDeploy/buildWithParameters?<br>CM_DIR=cm12345<br>&APP_NAME=MyWebApp<br>&token=01utcell&quot;`

Scroll down the page for a breakdown of each component.

`curl -X POST -k -u uid:yourJenkinsAPIToken`

These examples use the Linux [cURL] (https://curl.haxx.se/docs/manpage.html)  command to demonstrate use of the Jenkins API. Check the documentation for *your* client / language on how to submit HTTP POST requests.
The -X POST option ensures the request is send as an HTTP POST (not a GET).
The -k option for curl connects to the API endpoint without confirming SSL certificate validity. If you want to confirm the certificates validity, visit deploy.example.com in a browser and save the certificate from there, then use per your scripting client's documentation on SSL.</p>

Supply your userID (legacy hardware or legacy example), followed by a colon, followed by the [Jenkins API token associated with your userID](https://stackoverflow.com/questions/45466090/how-to-get-the-api-token-for-jenkins)

Protect your Jenkins API token as you would your password.
Using REST commands for a Jenkins Project requires the same authentication/authorization as running the Project in the Jenkins GUI

`"https://deploy.example.com/`


`https://deploy.example.com is the on-prem proxy endpoint that accepts the HTTP POST request. The proxy uses information in the request string (covered below) to route the request to the appropriate Jenkins instance
The double-quote before the URL is required, and is closed at the end of the URL (below)

`job/appDeploy/buildWithParameters?`

Jenkins API syntax for performing a build is `/job/JOBNAME/build`

`/job/JOBNAME/buildWithParameters` if the job takes parameters

[Jenkins Remote Access API Wiki] (https://wiki.jenkins.io/display/JENKINS/Remote+access+API) for more information, and examples of using JSON for parameters instead of name/value pairs

`CM_DIR=cm12345<br>&APP_NAME=MyWebApp<br>&token=wasv855-01utcell&quot`

These are the name/value parameters required by the JOBNAME
These can be viewed in the Jenkins GUI by clicking Build With Parameters within each JOBNAME (appDeploy, exampleappsDeploy, clusterStopStart, etc). Most of these are self-explanatory (CM folder, cluster, app name, etc.)\
token=<i>cellName</i> is required so the request gets routed to the Jenkins instance that serves the target cell. The cell names to use as token values can be seen in the Jenkins GUI in the description for each JOBNAME.

The double-quote at the end of the URL is required to enclose the URL.
