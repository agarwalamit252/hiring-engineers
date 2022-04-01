Note: I will be using ##answer as a divider for every answer to a question
Note: This is a computer I got from my mentor Jonathan Golding so you will see the host names and the name of the computer as Jonathan Golding. I haven't changed the name as I plan to return it to him someday.


Your answers to the questions go here.
1) Prerequisites - Setup the environment
You can utilize any OS/host that you would like to complete this exercise. However, we recommend one of the following approaches:
##answer 1
I first installed virtual box and then vagrant <img width="749" alt="Virtualbox with Vagrant" src="https://user-images.githubusercontent.com/102629064/161170325-0e893ac2-6b27-4073-8d05-933546fbeddc.png">

I then realized I need to learn how to set up environments for the datadog agent to run on, so I decided to move with installing datadog on the MacOS that I was using since datadog-agent is compatible with the MacOS <img width="1280" alt="Installing Datadog Agent" src="https://user-images.githubusercontent.com/102629064/161170488-710eac1a-4b6f-4fbf-b202-6c44c37bb8ee.png">

I made sure to use 'Datadog Recruiting Candidate' as Company Name <img width="954" alt="Datadog Recruiting Candidate" src="https://user-images.githubusercontent.com/102629064/161170787-1f149fc2-190e-4a90-a82c-522fd4053f11.png">

Agent Reporting Metrics
##answers
I found the metrics.yaml file to get the agent reporting metrics <img width="1280" alt="Agent Reporting Metrics Datadog" src="https://user-images.githubusercontent.com/102629064/161171172-61bff2bc-0095-47b4-9192-1c1b8f6ed9a9.png">

>>>>Collecting Metrics:
1) Add tags in the Agent config file and show us a screenshot of your host and its tags on the Host Map page in Datadog.
##answers
Using this: https://docs.datadoghq.com/getting_started/tagging/assigning_tags/?tab=noncontainerizedenvironments
I found the datadog.yaml file for tags and added tags such as city and team. On the second image the host tags I added show up on the host map. <img width="680" alt="Assigning Tags in Yaml" src="https://user-images.githubusercontent.com/102629064/161173087-db5e8ac4-b286-461a-99d3-f04fcc1f5514.png">
<img width="1272" alt="Host Tag Updated" src="https://user-images.githubusercontent.com/102629064/161177715-3f630ff2-2d91-49c3-94b0-ab71654b0425.png">


I then added tags on the host map. 
<img width="1280" alt="Host Tags and Host Name" src="https://user-images.githubusercontent.com/102629064/161173261-7a3d667a-5a51-4160-b253-4f4bcf364849.png">


2) Install a database on your machine (MongoDB, MySQL, or PostgreSQL) and then install the respective Datadog integration for that database.
##answers
I installed MySQL on my device 
<img width="729" alt="MYSQL Full Download" src="https://user-images.githubusercontent.com/102629064/161173557-00bf8c31-2dce-429a-ac6f-7a632e767ccc.png">
Then integrated it with the Datadog MySQL Integration https://docs.datadoghq.com/integrations/mysql/?tab=host#configuration. 
<img width="767" alt="MySQL Integration" src="https://user-images.githubusercontent.com/102629064/161173718-c3b8f255-bc95-4f6f-946a-43feb28b4ccd.png">

3) Create a custom Agent check that submits a metric named my_metric with a random value between 0 and 1000.
##answers
I used the document: https://docs.datadoghq.com/developers/custom_checks/write_agent_check/
I then researched the codes for generating random variables and import random came out. Below are the images with the codes
<img width="1279" alt="Metrics 1 - 1000" src="https://user-images.githubusercontent.com/102629064/161176067-3e4b69cc-349a-4b12-bb3a-821a2ef6337f.png">
<img width="582" alt="Metric 1 - 1000 code" src="https://user-images.githubusercontent.com/102629064/161176108-b8263b27-072c-4b8a-97c7-14f8eea9cbce.png">

4) Change your check's collection interval so that it only submits the metric once every 45 seconds.
Using this document: https://docs.datadoghq.com/developers/custom_checks/write_agent_check/#updating-the-collection-interval
I then went to the same custom_my_metric file and changed the interval to 45 sec. <img width="672" alt="My_Metric_45sec" src="https://user-images.githubusercontent.com/102629064/161176489-3fe67418-e78e-44d7-bcd1-8f46d40ac3d0.png">
<img width="373" alt="45 sec interval first picture time stamp" src="https://user-images.githubusercontent.com/102629064/161177020-28f832ed-74ab-4495-8d91-d7a14aef3e5e.png">
<img width="373" alt="45 sec interval second picture time stamp" src="https://user-images.githubusercontent.com/102629064/161177032-1b4c40ea-544f-411f-b072-55fdd1e62125.png">

Bonus Question Can you change the collection interval without modifying the Python check file you created?
##answer
Yes, we can make changes to the .yaml file and not change the .py file.

>>>>Visualizing Data:
Utilize the Datadog API to create a Timeboard that contains:
1) Your custom metric scoped over your host. I selected both the custom_my_metric and the system_cpu_user which I believe is the host<img width="1242" alt="Custom Metric over host" src="https://user-images.githubusercontent.com/102629064/161186292-5b71daa6-255c-4ed8-add9-6ca911552cbf.png">
I tried following the document with the api client: https://docs.datadoghq.com/api/latest/dashboards/#create-a-new-dashboard and basically copied the code that was given on the document and personalized it. When I ran the code it was giving me an error.I also created a Dashboard.yaml file after creating a Dashboard.py file (the one with the api client timeseries code). Not sure I did this one right.
<img width="868" alt="Timeboard Personalized Code" src="https://user-images.githubusercontent.com/102629064/161180209-630e4f51-4e99-4ab1-b809-97236e34f9ff.png">


2) Any metric from the Integration on your Database with the anomaly function applied.
##answer
I found this Datadog Doc: https://docs.datadoghq.com/monitors/create/types/anomaly/#anomaly-detection-algorithms and used that to overlay the anomoly over a mysql metric as MySQL was my integration with Datadog.
<img width="1107" alt="Anomoly Monitor Part 1" src="https://user-images.githubusercontent.com/102629064/161182981-549e38b4-ba06-4d5b-a40b-6c2a7df19eed.png">
<img width="1091" alt="Anomoly Monitor Part 2" src="https://user-images.githubusercontent.com/102629064/161182992-e850e6e2-7c3d-418b-a946-7effac3ad2e7.png">


3) Your custom metric with the rollup function applied to sum up all the points for the past hour into one bucket
Please be sure, when submitting your hiring challenge, to include the script that you've used to create this Timeboard.

##answer
I used this document for my rollup: https://docs.datadoghq.com/dashboards/querying/#rollup-to-aggregate-over-time
I click on the button the right of the aggregation group, then went to rollup, then click on sum, and then it gave me the option to select 1 hour. It is still collecting data.
<img width="373" alt="Custom_my_metric with roll up" src="https://user-images.githubusercontent.com/102629064/161184335-81fb7c55-5f9e-47d1-b18b-082bb2af17e6.png">
<img width="1252" alt="Custom_my_metric the actual configuration" src="https://user-images.githubusercontent.com/102629064/161184350-59d21b5e-02b2-4ee3-93bc-05e6a6430ebd.png">

------As stated in the question I am attaching the Script used to create custom_My_Metric:
import random
# the following try/except block will make the custom check compatible with any Agent version
try:
    # first, try to import the base class from new versions of the Agent...
    from datadog_checks.base import AgentCheck
except ImportError:
    # ...if the above failed, the check is running in Agent version < 6.6.0
    from checks import AgentCheck

# content of the special variable __version__ will be shown in the Agent status page
__version__ = "1.0.0"

class HelloCheck(AgentCheck):
    def check(self, instance):
        self.gauge('custom_my_metric',random.randint(0, 1000), tags=['host:jonathangolding'] + self.instance.get('tags', []))
---------

4) Once this is created, access the Dashboard from your Dashboard List in the UI:

  a) Set the Timeboard's timeframe to the past 5 minutes
##answer
I changed the value from global time to past 5 min <img width="1067" alt="Timeboard 5 min" src="https://user-images.githubusercontent.com/102629064/161185124-3343b976-d994-49fb-ade0-6caa8df36326.png">

b) Take a snapshot of this graph and use the @ notation to send it to yourself.
I did. As you will see in the image above I sent it to my email.
c) Bonus Question: What is the Anomaly graph displaying?
As stated in this document, an anomoly graph is supposed to show which points are going above or below the upper bound or the lower bound that is set by the anomoly graph. https://docs.datadoghq.com/monitors/create/types/anomaly/#anomaly-detection-algorithms
The anomoly graph is displaying a gray band which probably is the upper bound and the lower bound around the blue line which is the main graph line. I noticed it turned red, which I am assuming means that there was an anomaly where the numbers exceeded or crossed the gray band.

>>>>Monitoring Data
Since you’ve already caught your test metric going above 800 once, you don’t want to have to continually watch this dashboard to be alerted when it goes above 800 again. So let’s make life easier by creating a monitor.
a) Create a new Metric Monitor that watches the average of your custom metric (my_metric) and will alert if it’s above the following values over the past 5 minutes:
Warning threshold of 500
Alerting threshold of 800
And also ensure that it will notify you if there is No Data for this query over the past 10m.
##answer
The monitor gave me options to set up the alerting conditions. Here is the picture: <img width="1224" alt="Setting Thresholds 800 and 500" src="https://user-images.githubusercontent.com/102629064/161187964-d31f6cc2-eae2-4c26-a709-dacecff82dcf.png">

b) Please configure the monitor’s message so that it will:

---->Send you an email whenever the monitor triggers.
  Create different messages based on whether the monitor is in an Alert, Warning, or No Data state.
  Include the metric value that caused the monitor to trigger and host ip when the Monitor triggers an Alert state.
##answer
I set up alert properties with some templates and the key words of alert, warn and is_no_data. <img width="1243" alt="Alert Properties" src="https://user-images.githubusercontent.com/102629064/161188825-977f09aa-fe0a-40a0-a6e0-1c6d602d4175.png">

----->When this monitor sends you an email notification, take a screenshot of the email that it sends you.
##answer
<img width="817" alt="Email notification of alert" src="https://user-images.githubusercontent.com/102629064/161189088-a3d85382-72db-4ce7-a1ae-61e6793a01d9.png">

------>Bonus Question: Since this monitor is going to alert pretty often, you don’t want to be alerted when you are out of the office. Set up two scheduled downtimes for this monitor:

----->One that silences it from 7pm to 9am daily on M-F,
##answer
I changed the RRule. <img width="640" alt="Downtime 7pm - 9am Custom Metric" src="https://user-images.githubusercontent.com/102629064/161189661-f8861287-823b-4c3c-a2f6-f3e5896821c9.png"> Document that helped me: https://icalendar.org/iCalendar-RFC-5545/3-8-5-3-recurrence-rule.html

----->And one that silences it all day on Sat-Sun.
##answer
I changed the RRule <img width="640" alt="Downtime Weekend" src="https://user-images.githubusercontent.com/102629064/161190618-54ee4127-2a21-45ed-a770-4f73ba109f2d.png">

----->Make sure that your email is notified when you schedule the downtime and take a screenshot of that notification.
##answer
Downtime notifications:
7pm to 9pm Mon - Fri <img width="791" alt="Downtime notification for 7pm" src="https://user-images.githubusercontent.com/102629064/161190828-0f16787c-6c6a-468c-b746-a27217cf9248.png">
Weekend - <img width="791" alt="Downtime notification weekend" src="https://user-images.githubusercontent.com/102629064/161190897-2e43e1cc-4202-4c91-82ec-9c6c2e3aa9fc.png">

>>>>>>>>>Collecting APM Data:
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
Note: Using both ddtrace-run and manually inserting the Middleware has been known to cause issues. Please only use one or the other.


1) ##answer
I used this document to first install ddtrace: https://docs.datadoghq.com/tracing/setup_overview/setup/python/?tab=containers. https://app.datadoghq.com/apm/docs?architecture=host-based&language=python
Here are the updates: 
Getting the dd trace code after installing dd trace: <img width="826" alt="DD Trace" src="https://user-images.githubusercontent.com/102629064/161191405-b5fce264-2498-4611-8951-ba31050f6ef2.png">

In order to use flask as mentioned in the question I needed to install it first so I used pip3 intall flask: <img width="785" alt="Instaling Flask" src="https://user-images.githubusercontent.com/102629064/161193232-0df3a07e-8538-449d-ab8d-9a808b9a2fb6.png">

Created my_app.py python file as that was in the DD code and I put in the flask code provided in it: <img width="566" alt="Created myapp py file" src="https://user-images.githubusercontent.com/102629064/161192892-ab7b7c56-03cb-440c-bae6-d42008bb6e70.png">

This led to: <img width="821" alt="DD Trace Accomplished!" src="https://user-images.githubusercontent.com/102629064/161193326-0af9cbba-9384-46fe-94bf-9bc82a040126.png">
I copied the http link: <img width="510" alt="DD Trace HTTP" src="https://user-images.githubusercontent.com/102629064/161193358-99daca3d-c63e-4f25-9817-b8115945aaf2.png">

As per the instructions I restarted datadog agent and re-entered the DD_SERVICE="DD_Sales_Engineer" DD_ENV="<Datadog> python3 my_app.py: <img width="991" alt="DD-Trace-Final" src="https://user-images.githubusercontent.com/102629064/161193755-cf4c9bcd-b3f8-4fa0-b600-46045679aa77.png">

Datadog Agent Status to show APM - <img width="479" alt="Trace Agent Datadog Status" src="https://user-images.githubusercontent.com/102629064/161194328-b5a7e282-74b1-48e9-8f68-02124ecbad2a.png">

I was not able to finish step 5 of the APM which is probably why when I go to APM is just says get started. That is the command I ran from the document:export DD_ENV="Datadog" DD_SERVICE="DD_Sales_Engineer" DD_VERSION="0.38.0+" /bin/my-DD_Sales_Engineer
  
I also put the run time metrics directly into the my_app.py where APM is running. Still the APM on Datadog Web is not showing anything. On the python shell it shows that run time metrics are working!
  Python Shell Run-time Metrics: <img width="1087" alt="Python Shell Run Time Metrics" src="https://user-images.githubusercontent.com/102629064/161200057-44ad79d9-819e-4c92-904f-5ebe019eebab.png">
  <img width="924" alt="RunTime Metrics" src="https://user-images.githubusercontent.com/102629064/161198792-b1934db4-ce6b-403e-9330-4abd67cf2b33.png">


 2) Bonus Question: What is the difference between a Service and a Resource?
  A resource is a particular domain of a customer application - they are typically an instrumented web endpoint, database query, or background job.As per the document. So basically they are tools for a service. For example when we created the alerting thresholds, those are resources. Services are the building blocks of modern microservice architectures. For example an APM Webstore is a service for monitoring latency and other variables.
  
  https://docs.datadoghq.com/tracing/visualization/resource/
  

3) Provide a link and a screenshot of a Dashboard with both APM and Infrastructure Metrics.
  
  Link to Host Cloned Dashboard: https://app.datadoghq.com/dashboard/8xe-2gp-id3/jonathans-macbooklocal-cloned-showing-apm-metrics?from_ts=1648784331025&to_ts=1648787931025&live=true
  
Screenshot of Dashboard:  <img width="1227" alt="Cloned_Dashboard_Amit" src="https://user-images.githubusercontent.com/102629064/161200129-965b1861-cc1b-48fd-8c78-a67020b7b37e.png">


Please include your fully instrumented app in your submission, as well.
  
>>>>>>>>>>>Final Question:
Datadog has been used in a lot of creative ways in the past. We’ve written some blog posts about using Datadog to monitor the NYC Subway System, Pokemon Go, and even office restroom availability!

Is there anything creative you would use Datadog for?
##answer
Here is a cool idea. We all know that waste management is inefficient. At the moment through Datadog Agents we can track the inflows of traffic on a website. It would be wonderful if we could install Datadog Agents in cars that transport waste. This way we could track the inefficiencies in routes for drivers, and visualize that on the graph. Furhtermore, we could put APM's on the waster collecting machines to somehow see the exact amount of waste generated per day, week, month, year. This is still a little broad but I am sure DataDog's unified platform would tremendously help with waste mangement.
  
----------
Ending Note:

What a journey this has been. I have learned so much!!! Wow! I can see why DataDog would benefit so many organizations especially with its intuitive graphs. My confidence and morale have boosted so much. I do have a long way to go to understand all of DataDogs' products deeply, and I believe this is a great introduction to my journey.
  
Thank you for giving me the opportunity and I really mean it, to take this assessment. It was inspiring to know that I can rapidly learn from a variety of sources.
  
Thanks Amanda, Don and Edwin, and I look forward to my next steps.


