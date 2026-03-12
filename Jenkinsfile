pipeline {
agent any
 triggers {
 pollSCM(&#39;* * * * *&#39;)
 }
 environment {
 IMAGE_NAME = &quot;devops-app&quot;
 CONTAINER_NAME = &quot;devops-container&quot;
 APP_PORT = &quot;5000&quot;
 }
stages {
 stage(&#39;Build Docker Image&#39;) {
 steps {
 bat &quot;docker build --no-cache -t %IMAGE_NAME% .&quot;
 }
 }
 stage(&#39;Stop Existing Containers&#39;) {
steps {

 bat &#39;&#39;&#39;
 for /f &quot;tokens=*&quot; %%i in (&#39;docker ps -q&#39;) do docker stop %%i
for /f &quot;tokens=*&quot; %%i in (&#39;docker ps -aq&#39;) do docker rm %%i
 &#39;&#39;&#39;
 }
 }
 stage(&#39;Run New Container&#39;) {
 steps {
 bat &quot;docker run -d --name %CONTAINER_NAME% -p
%APP_PORT%:%APP_PORT% %IMAGE_NAME%&quot;
 }
 }
 }
}