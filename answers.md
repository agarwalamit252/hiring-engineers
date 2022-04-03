Note: I will be using ##answer as a divider for every answer to a question
Note: This is a computer I got from my mentor Jonathan Golding so you will see the host names and the name of the computer as Jonathan Golding. I haven't changed the name as I plan to return it to him someday. I have labelled sections accordingly as Section 1, 2, 3, 4 and 5 starting with Collecting Metrics.


Your answers to the questions go here.
1) Prerequisites - Setup the environment
You can utilize any OS/host that you would like to complete this exercise. However, we recommend one of the following approaches:

##answer: 
So I first had to read the assessment several times, like almost 6 times. I had some experience with VMWare but not Virtualbox which is also a VM offered by Oracle. Since this was one of the recommended ways, and I didn't have a containerized environment like Docker, I decided to learn how to install Virtual Box, Vagrant and then set up an environment for the datadog agent. This document helped me: https://learn.hashicorp.com/collections/vagrant/getting-started

The document did say that my virutal box would have 18.04 already installed. So naturally I expected Ubuntu to open when I click start on the virtual box. Yet nothing was happening. I was only seeing a black screen. <img width="739" alt="Vagrant Black Screen" src="https://user-images.githubusercontent.com/102629064/161291564-b674deef-7f68-4066-bf11-c546d7a9ab68.png">


I think Ubuntu was just pretty slow in opening so I moved to installing the Datadog Agent directly onto the MacOS that I was using since datadog-agent is compatible with the MacOS to complete the project. I went to https://www.datadoghq.com/ as advised on the assignment. It was really cool to see a colorful and modern looking website. I entered my details, signed up for a trial and on the get started page I followed the instructions to install the Datadog Agent v7. The agent page asked me to choose my OS, and I selected MAC OS. The instructions to launch the datadog agent v7 was: DD_AGENT_MAJOR_VERSION=7 DD_API_KEY=fb3f61f89c8a8a4046ff1bd97b0e6040 DD_SITE="datadoghq.com" bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_mac_os.sh)" from the integrations page when I signed up for the trial.

I copied and pasted than in the terminal and then it installed the datadog agent on my MacOS. <img width="1280" alt="Installing Datadog Agent" src="https://user-images.githubusercontent.com/102629064/161170488-710eac1a-4b6f-4fbf-b202-6c44c37bb8ee.png">

I made sure to use 'Datadog Recruiting Candidate' as Company Name <img width="954" alt="Datadog Recruiting Candidate" src="https://user-images.githubusercontent.com/102629064/161170787-1f149fc2-190e-4a90-a82c-522fd4053f11.png">

Agent Reporting Metrics

##answers
I didn't necessarily know how to find the agent reporting metrics but I knew 'local machine' meant that there must be a file or folder on the local machine. So I began my manual search. It took a long time. This was really helpful as I got to understand the whole folder that datadog installs. I finally discovered the hidden 'opt' folder that had the 'datadog agent'. I opened folder by folder, and saw the conf.d folder. That had a lot of .yaml files. I knew it was inefficient to open all the folders, so I selected all folders and expanded them at the same time using 'command + a' and then 'command+shift+right arrow'. I finally found the metrics.yaml file to get the agent reporting metrics by scrolling. <img width="1280" alt="Agent Reporting Metrics Datadog" src="https://user-images.githubusercontent.com/102629064/161171172-61bff2bc-0095-47b4-9192-1c1b8f6ed9a9.png">

>>>>SECTION 1: Collecting Metrics:

1) Add tags in the Agent config file and show us a screenshot of your host and its tags on the Host Map page in Datadog.

##answers
I searched google for how to assign tags datadog and this document showed up:
Using this: https://docs.datadoghq.com/getting_started/tagging/assigning_tags/?tab=noncontainerizedenvironments
The document asked me to navigate to the datadog.yaml file. I found the datadog.yaml file for tags, as I had done a lot searching on the conf.d folder previously already, and added tags such as city and team. I then went to the Datadog account and went through each tab on the left. One of them said 'infrastructure', and beside that was 'Host Map'. I thought that must be it! It gave me an option to click on 'agent' which is the agent I just installed. It then asked me to 'edit tags' which was straightforward. On the second image the host tags I added show up on the host map. <img width="680" alt="Assigning Tags in Yaml" src="https://user-images.githubusercontent.com/102629064/161173087-db5e8ac4-b286-461a-99d3-f04fcc1f5514.png">
<img width="1272" alt="Host Tag Updated" src="https://user-images.githubusercontent.com/102629064/161177715-3f630ff2-2d91-49c3-94b0-ab71654b0425.png">


Picture for tags on the host map. 
<img width="1280" alt="Host Tags and Host Name" src="https://user-images.githubusercontent.com/102629064/161173261-7a3d667a-5a51-4160-b253-4f4bcf364849.png">


2) Install a database on your machine (MongoDB, MySQL, or PostgreSQL) and then install the respective Datadog integration for that database.

##answers
It was a tough choice as I didn't know which one to install. In my work I didn't use either. I had used MySQL in the past, and because of familiarity I decided to go with MySQL. I searched youtube on how to install MySQL. Here are the two links I followed:
https://www.youtube.com/watch?v=-BDbOOY9jsc
https://www.youtube.com/watch?v=UcpHkYfWarM
I installed MySQL on my device according to the instructions.
<img width="729" alt="MYSQL Full Download" src="https://user-images.githubusercontent.com/102629064/161173557-00bf8c31-2dce-429a-ac6f-7a632e767ccc.png">

After installation I had to create a profile for MySQL as explained in the video. Using mysql -u root -p I could finally launch mysql from the terminal. It then will ask you for a password, and then I was good to go!

The next part on the assignment was integrating MySQL with Datadog. So I went over to the integrations page and found the MySQL integration.
I followed the steps from Datadog MySQL Integration https://docs.datadoghq.com/integrations/mysql/?tab=host#configuration. After preparing MySQL as per the document, you will also need to create the folder mysql.d and file conf.yaml on the conf.d folder. You can do it from the terminal itself. Locate the conf.d folder cd ~/.datadog-agent/conf.d/. Then open the new file with: nano mysql.d/conf.yaml. Then put the contents of the host configuration section in this document. I had to change the pass and port. Now as per the document, I restarted datadog agent by datadog-agent stop and then datadog-agent start. I then checked online on the Datadog account to see if there were any changes, and there was an update on the integrations pages saying I successfully installed MySQL!
<img width="767" alt="MySQL Integration" src="https://user-images.githubusercontent.com/102629064/161173718-c3b8f255-bc95-4f6f-946a-43feb28b4ccd.png">

3) Create a custom Agent check that submits a metric named my_metric with a random value between 0 and 1000.

##answers
I used the document: https://docs.datadoghq.com/developers/custom_checks/write_agent_check/
I then researched the codes for generating random variables and import random came out. Below are the images with the codes
<img width="1279" alt="Metrics 1 - 1000" src="https://user-images.githubusercontent.com/102629064/161176067-3e4b69cc-349a-4b12-bb3a-821a2ef6337f.png">
<img width="582" alt="Metric 1 - 1000 code" src="https://user-images.githubusercontent.com/102629064/161176108-b8263b27-072c-4b8a-97c7-14f8eea9cbce.png">

4) Change your check's collection interval so that it only submits the metric once every 45 seconds.

##answers
Using this document: https://docs.datadoghq.com/developers/custom_checks/write_agent_check/#updating-the-collection-interval
I created a file named custom_my__metric.yaml on the conf.d folder. You can do it directly from the Mac GUI, or you can do it from the terminal. I chose to do it from the Mac folder directly as clicking and navigating folders is definitely easier for me. I put the code into the folder like the document says on the interval section. I modified the interval to 45 seconds. I then create a custom_my_metric.py file. The question was how do I modify the code so that it generates random integrers. From googling I got to know that I had to import random module. Now the results section of this doc: https://docs.datadoghq.com/developers/custom_checks/write_agent_check/ really helped me modify the code. Instead of file count, I had to substitute the code for random integers. Using this document: https://docs.python.org/3/library/random.html I found the code: random.randint(). After I put the code in I restarted the agent. On the metrics section on the Datadog Account, I click on explorer and typed my file name custom_my_metric and it showed up! I was really happy this happened.
<img width="672" alt="My_Metric_45sec" src="https://user-images.githubusercontent.com/102629064/161176489-3fe67418-e78e-44d7-bcd1-8f46d40ac3d0.png">
<img width="373" alt="45 sec interval first picture time stamp" src="https://user-images.githubusercontent.com/102629064/161177020-28f832ed-74ab-4495-8d91-d7a14aef3e5e.png">
<img width="373" alt="45 sec interval second picture time stamp" src="https://user-images.githubusercontent.com/102629064/161177032-1b4c40ea-544f-411f-b072-55fdd1e62125.png">

Bonus Question Can you change the collection interval without modifying the Python check file you created?

##answer
Yes, we can make changes to the .yaml file and not change the .py file.

>>>>SECTION 2: Visualizing Data:

Utilize the Datadog API to create a Timeboard that contains:
1) Your custom metric scoped over your host. 

##answer
I first created a dashboard with the custom_my_metric. I selected both the custom_my_metric and the system_cpu_user which I believe is the host.
<img width="1242" alt="Custom Metric over host" src="https://user-images.githubusercontent.com/102629064/161186292-5b71daa6-255c-4ed8-add9-6ca911552cbf.png">
The question does ask me to create a timeboard from the api client so I google datadog timeboard api client. I tried following the document with the api client: https://docs.datadoghq.com/api/latest/dashboards/#create-a-new-dashboard and basically copied the code that was given on the document and personalized it. I first installed the libaray on terminal and then imported the datadog api client on python. I save the code from the document on Dashboard.py. I rant the code, DD_SITE="datadoghq.com" DD_API_KEY="fb3f61f89c8a8a4046ff1bd97b0e6040" DD_APP_KEY="12714d38e2aceb095ca96763398f5af8913c2113" python3 "Dashboard.py" but it continously gave me an error.I also created a Dashboard.yaml file after creating a Dashboard.py file (the one with the api client timeseries code). Not sure I did this one right.
<img width="868" alt="Timeboard Personalized Code" src="https://user-images.githubusercontent.com/102629064/161180209-630e4f51-4e99-4ab1-b809-97236e34f9ff.png">


2) Any metric from the Integration on your Database with the anomaly function applied.

##answer
I googeled and found this Datadog Doc: https://docs.datadoghq.com/monitors/create/types/anomaly/#anomaly-detection-algorithms and used that to overlay the anomoly over a mysql metric as MySQL was my integration with Datadog. I went to Monitors –> New Monitor –> Anomaly. I then selected a mysql metric. The pictures below show the result and a gray band over the evaluation review.
<img width="1107" alt="Anomoly Monitor Part 1" src="https://user-images.githubusercontent.com/102629064/161182981-549e38b4-ba06-4d5b-a40b-6c2a7df19eed.png">
<img width="1091" alt="Anomoly Monitor Part 2" src="https://user-images.githubusercontent.com/102629064/161182992-e850e6e2-7c3d-418b-a946-7effac3ad2e7.png">


3) Your custom metric with the rollup function applied to sum up all the points for the past hour into one bucket
Please be sure, when submitting your hiring challenge, to include the script that you've used to create this Timeboard.

##answer
I used this document for my rollup: https://docs.datadoghq.com/dashboards/querying/#rollup-to-aggregate-over-time
I click on the button the right of the aggregation group on my custom_my_metric dashboard, then went to rollup, then click on sum, and then it gave me the option to select 1 hour. It is collecting data.

<img width="373" alt="Custom_my_metric with roll up" src="https://user-images.githubusercontent.com/102629064/161184335-81fb7c55-5f9e-47d1-b18b-082bb2af17e6.png">

<img width="1252" alt="Custom_my_metric the actual configuration" src="https://user-images.githubusercontent.com/102629064/161184350-59d21b5e-02b2-4ee3-93bc-05e6a6430ebd.png">

-As stated in the question I am attaching the Script used to create custom_My_Metric:
<img width="582" alt="Custom_My_Metric Script" src="https://user-images.githubusercontent.com/102629064/161205252-ebdbe026-663a-4e3c-9ab0-5675535a8126.png">


4) Once this is created, access the Dashboard from your Dashboard List in the UI:

a)Set the Timeboard's timeframe to the past 5 minutes

##answer: I click on the edit button on the custom_my_metric dashboard and changed the value from global time to past 5 min <img width="1067" alt="Timeboard 5 min" src="https://user-images.githubusercontent.com/102629064/161185124-3343b976-d994-49fb-ade0-6caa8df36326.png">

b) Take a snapshot of this graph and use the @ notation to send it to yourself.

##answer: I did. As you will see in the image above I sent it to my email.

c) Bonus Question: What is the Anomaly graph displaying?

##answer: As stated in this document, an anomoly graph is supposed to show which points are going above or below the upper bound or the lower bound that is set by the anomoly graph. https://docs.datadoghq.com/monitors/create/types/anomaly/#anomaly-detection-algorithms
The anomoly graph is displaying a gray band which probably is the upper bound and the lower bound around the blue line which is the main graph line. I noticed it turned red, which I am assuming means that there was an anomaly where the numbers exceeded or crossed the gray band.

>>>> SECTION 3: Monitoring Data

Since you’ve already caught your test metric going above 800 once, you don’t want to have to continually watch this dashboard to be alerted when it goes above 800 again. So let’s make life easier by creating a monitor.

a) Create a new Metric Monitor that watches the average of your custom metric (my_metric) and will alert if it’s above the following values over the past 5 minutes:
Warning threshold of 500
Alerting threshold of 800
And also ensure that it will notify you if there is No Data for this query over the past 10m.

##answer
The keyword was monitor here. So after playing around with the dashboard, I clicked on setting and found an option named 'create monitor'. That led me right to the monitor for custom_my_metric. I then opened the monitor and clicked on the edit button under settings. The monitor gave me options to set up the alerting conditions. Here is the picture: <img width="1224" alt="Setting Thresholds 800 and 500" src="https://user-images.githubusercontent.com/102629064/161187964-d31f6cc2-eae2-4c26-a709-dacecff82dcf.png">

b) Please configure the monitor’s message so that it will: 

Q: Send you an email whenever the monitor triggers.
Create different messages based on whether the monitor is in an Alert, Warning, or No Data state.
Include the metric value that caused the monitor to trigger and host ip when the Monitor triggers an Alert state.

##answer
I set up alert properties with some templates and the key words of alert, warn and is_no_data. I treated each segment of alert, warn and no data as an if statement. I found commands like threshold, is_nodata, warn_threshold. It took a lot of detailed additions of the code but eventually the code made sense. <img width="1243" alt="Alert Properties" src="https://user-images.githubusercontent.com/102629064/161188825-977f09aa-fe0a-40a0-a6e0-1c6d602d4175.png">

At the  configuration page of the monitor it gave me an option to add my email so I would get notified.

Q: When this monitor sends you an email notification, take a screenshot of the email that it sends you.

##answer
<img width="817" alt="Email notification of alert" src="https://user-images.githubusercontent.com/102629064/161189088-a3d85382-72db-4ce7-a1ae-61e6793a01d9.png">

Bonus Question: Since this monitor is going to alert pretty often, you don’t want to be alerted when you are out of the office. Set up two scheduled downtimes for this monitor:

a) One that silences it from 7pm to 9am daily on M-F,

##answer
In order to do this, I saw from the dropdown on the monitor tab, an option called, 'manage downtimes'. I clicked on that and it gave me an option to schedule downtime. That is what I needed. Then I selected the custom_my_metric monitor from the dropdown, and then learned to set the conditions by changing the RRule. Document that helped me: https://icalendar.org/iCalendar-RFC-5545/3-8-5-3-recurrence-rule.html <img width="640" alt="Downtime 7pm - 9am Custom Metric" src="https://user-images.githubusercontent.com/102629064/161189661-f8861287-823b-4c3c-a2f6-f3e5896821c9.png"> 

b) And one that silences it all day on Sat-Sun.

##answer
I created a new downtime schedule and changed the RRule just like the above <img width="640" alt="Downtime Weekend" src="https://user-images.githubusercontent.com/102629064/161190618-54ee4127-2a21-45ed-a770-4f73ba109f2d.png">

----->Make sure that your email is notified when you schedule the downtime and take a screenshot of that notification.

##answer
Downtime notifications:

7pm to 9pm Mon - Fri: <img width="791" alt="Downtime notification for 7pm" src="https://user-images.githubusercontent.com/102629064/161190828-0f16787c-6c6a-468c-b746-a27217cf9248.png">

Weekend - <img width="791" alt="Downtime notification weekend" src="https://user-images.githubusercontent.com/102629064/161190897-2e43e1cc-4202-4c91-82ec-9c6c2e3aa9fc.png">

>>>> SECTION 4: Collecting APM Data:

Given the following Flask app (or any Python/Ruby/Go app of your choice) instrument this using Datadog’s APM solution:

from flask import Flask
import logging
import sys

# Have flask use stdout as the logger
main_logger = logging.getLogger()
main_logger.setLevel(logging.DEBUG)
c = logging.StreamHandler(sys.stdout)
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
c.setFormatter(formatter)
main_logger.addHandler(c)

app = Flask(__name__)

@app.route('/')
def api_entry():
    return 'Entrypoint to the Application'

@app.route('/api/apm')
def apm_endpoint():
    return 'Getting APM Started'

@app.route('/api/trace')
def trace_endpoint():
    return 'Posting Traces'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port='5050')
    
    
1) Note: Using both ddtrace-run and manually inserting the Middleware has been known to cause issues. Please only use one or the other.

##answer: So I needed to understand the problem first. It was asking me to enable tracing on my_app.py which has the code given above. I used this document to first install ddtrace: https://docs.datadoghq.com/tracing/setup_overview/setup/python/?tab=containers. https://app.datadoghq.com/apm/docs?architecture=host-based&language=python
Here are the updates: 
Getting the dd trace code after installing dd trace: <img width="826" alt="DD Trace" src="https://user-images.githubusercontent.com/102629064/161191405-b5fce264-2498-4611-8951-ba31050f6ef2.png">

In order to use flask as mentioned in the question I needed to install it first so I used pip3 install flask: <img width="785" alt="Instaling Flask" src="https://user-images.githubusercontent.com/102629064/161193232-0df3a07e-8538-449d-ab8d-9a808b9a2fb6.png">

Created my_app.py python file as that was in the DD code and I put in the flask code provided in it: <img width="566" alt="Created myapp py file" src="https://user-images.githubusercontent.com/102629064/161192892-ab7b7c56-03cb-440c-bae6-d42008bb6e70.png">

This led to: <img width="821" alt="DD Trace Accomplished!" src="https://user-images.githubusercontent.com/102629064/161193326-0af9cbba-9384-46fe-94bf-9bc82a040126.png">

I copied the http link: <img width="510" alt="DD Trace HTTP" src="https://user-images.githubusercontent.com/102629064/161193358-99daca3d-c63e-4f25-9817-b8115945aaf2.png">

As per the instructions I restarted datadog agent and re-entered the DD_SERVICE="DD_Sales_Engineer" DD_ENV="<Datadog> python3 my_app.py: <img width="991" alt="DD-Trace-Final" src="https://user-images.githubusercontent.com/102629064/161193755-cf4c9bcd-b3f8-4fa0-b600-46045679aa77.png">

Datadog Agent Status to show APM - <img width="479" alt="Trace Agent Datadog Status" src="https://user-images.githubusercontent.com/102629064/161194328-b5a7e282-74b1-48e9-8f68-02124ecbad2a.png">

Python Shell Run-time Metrics: <img width="1087" alt="Python Shell Run Time Metrics" src="https://user-images.githubusercontent.com/102629064/161200057-44ad79d9-819e-4c92-904f-5ebe019eebab.png">
<img width="924" alt="RunTime Metrics" src="https://user-images.githubusercontent.com/102629064/161198792-b1934db4-ce6b-403e-9330-4abd67cf2b33.png">

Now the final few parts:

Here are the documents I used:
    https://docs.datadoghq.com/getting_started/tagging/unified_service_tagging/?tab=kubernetes#non-containerized-environment
    https://docs.datadoghq.com/getting_started/tracing/
    https://docs.datadoghq.com/tracing/guide/send_traces_to_agent_by_api/
    
From the datadog.yaml file I need to add or change configurations under the APM configuration. I read: https://docs.datadoghq.com/tracing/troubleshooting/
https://docs.datadoghq.com/tracing/troubleshooting/connection_errors/. I went to the datadog.yaml file and went to the APM Section. I enabled APM and configured the receiving port. I also added tags for DD_ENV: Datadog, and DD_SERVIE: DD_SALES_ENGINEER. I checkED the port from Datadog-agent status. The port seems to be running fine.<img width="363" alt="APM Status" src="https://user-images.githubusercontent.com/102629064/161323123-51418fbb-abc8-41af-ad15-fb541b2987d9.png">

To send traces from the local machine to DataDog APM, I ran a curl command. curl -X PUT "http://localhost:8126/v0.3/traces" \
with the configuration: <img width="579" alt="Curl Command" src="https://user-images.githubusercontent.com/102629064/161340514-19c9e890-dd37-496e-b533-81e8d482266e.png">

Here is the result of the curl command: <img width="1116" alt="APM Curl Command Results" src="https://user-images.githubusercontent.com/102629064/161340709-0c528085-3aac-4e6a-ac58-9ae5f198f694.png">
    
I know traces still need to flow into the DataDog agent and I think this will be a learning for me. I feel like I am really close but just not there.
    
I have an update on this! I finally figured it out. I made it complicated with the curl command before. I simply had to use this: curl http://0.0.0.0:5050/ and follow the instructions before from: https://docs.datadoghq.com/getting_started/tracing/
    
Here is the updated screenshots of my coding and the result on Datadog APM.
    1) export DD_SERVICE=my_app DD_ENV=Datadog DD_VERSION=flask DD_LOGS_INJECTION=true 
    2) ddtrace-run python3 my_app.py
    3) Screenshot: <img width="1230" alt="Exporting and DDTrace Run" src="https://user-images.githubusercontent.com/102629064/161442975-52f69017-9c09-41ad-b6df-99d3c892a75d.png">
    
    4) Then I simply had to run the curl command and start the datadog agent: curl http://0.0.0.0:5050/
    5) datadog-agent start
    6) screenshot:   <img width="709" alt="Curl command and starting agent" src="https://user-images.githubusercontent.com/102629064/161443042-eba9a899-9a54-4f98-abcb-472b33c2d682.png">
    
    Now lets look at the services page on APM: <img width="1277" alt="Services page" src="https://user-images.githubusercontent.com/102629064/161443328-8cd086f1-8e75-4c91-93c5-be87892df0c2.png">

    <img width="1093" alt="Traces" src="https://user-images.githubusercontent.com/102629064/161443337-28598863-99e2-4fb1-92dd-52c1c91d1cbd.png">


2) Bonus Question: What is the difference between a Service and a Resource?
  
##answer: A resource is a particular domain of a customer application - they are typically an instrumented web endpoint, database query, or background job.As per the document. So basically they are tools for a service. For example when we created the alerting thresholds, those are resources. Services are the building blocks of modern microservice architectures. For example an APM Webstore is a service for monitoring latency and other variables.
  
https://docs.datadoghq.com/tracing/visualization/resource/



3) Provide a link and a screenshot of a Dashboard with both APM and Infrastructure Metrics.
  
##answer: Link to Host Cloned Dashboard: https://app.datadoghq.com/dashboard/8xe-2gp-id3/jonathans-macbooklocal-cloned-showing-apm-metrics?from_ts=1648784331025&to_ts=1648787931025&live=true
  
Screenshot of Dashboard: <img width="1272" alt="Dashboard Screenshot" src="https://user-images.githubusercontent.com/102629064/161443418-a6347748-67b6-448c-8066-290429dc1510.png">


Please include your fully instrumented app in your submission, as well.

>>>> SECTION 5: Final Question:

Datadog has been used in a lot of creative ways in the past. We’ve written some blog posts about using Datadog to monitor the NYC Subway System, Pokemon Go, and even office restroom availability!

Is there anything creative you would use Datadog for?

##answer
Here is a cool idea. We all know that waste management is inefficient. At the moment through Datadog Agents we can track the inflows of traffic on a website. It would be wonderful if we could install Datadog Agents in cars that transport waste. This way we could track the inefficiencies in routes for drivers, and visualize that on the graph. Furhtermore, we could put APM's on the waster collecting machines to somehow see the exact amount of waste generated per day, week, month, year. This is still a little broad but I am sure DataDog's unified platform would tremendously help with waste mangement.
  



----------
Ending Note:

What a journey this has been. I have learned so much!!! Wow! I can see why DataDog would benefit so many organizations especially with its intuitive graphs. My confidence and morale have boosted so much. I do have a long way to go to understand all of DataDogs' products deeply, and I believe this is a great introduction to my journey.
  
Thank you for giving me the opportunity and I really mean it, to take this assessment. It was inspiring to know that I can rapidly learn from a variety of sources.
  
Thanks Amanda, Don and Edwin, and I look forward to my next steps.


