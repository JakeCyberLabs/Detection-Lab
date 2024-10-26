# Detection Lab
Detecting nmap scans using the SIEM tool Elastic

## Objective

The Detection Lab project aimed to establish a controlled environment for simulating and detecting security-related events. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen understanding of using the SIEM tool Elastic by creating dashboards and rules to detect security-related events.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in dashboard and alert creation. 
- Ability to generate and recognize security-related events.
- Enhanced knowledge of the Elastic SIEM tool.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Kali Linux virtual machine

## Steps
drag & drop screenshots here or use imgur and reference them using imgsrc

 - First, i will head over to Elastic and create an account so i can utilize this SIEM tool.

- Once i have created an account, i will configure a deployment and select "Elasticsearch" as the deployment type.

- When the configuration is complete, i will spin up a Kali Linux virtual machine so i can set up an agent to collect and forward the security-related logs from.

- I will head back over to Elastic to setup the agent that i will download onto my virtual machine.

- From here, i navigate to the integrations page by clicking on the Kibana main menu bar at the top left, then selecting "integrations" at the bottom.

    ![image](https://github.com/user-attachments/assets/e5c58d2e-71fb-476f-88c8-114ad8a6a8ac)

- i then search for "Elastic Defend" and click on it to open the integrations page.

  
   ![image](https://github.com/user-attachments/assets/315f2323-99d8-49cc-bed4-e32d94caa2dc)


- I then click on "Install Elastic Defend" and follow the instructions provided on the integrations page to install the agent on my Kali VM.

  
   ![image](https://github.com/user-attachments/assets/19e2a1df-f615-478e-8542-716f3928b5e6)


- I will paste the following command into the Kali terminal

  
   ![image](https://github.com/user-attachments/assets/2aec615d-2aac-4328-bef9-a4f7c3db43b3)

  
   ![image](https://github.com/user-attachments/assets/db1951e8-ed95-41e4-a142-c92257d3cc25)


- Once the agent is installed, it will automatically start collecting and forwarding logs to my Elastic SIEM instance.
- To verify that the agent is working correctly, i will generate some security-related events onto my Kali VM. To do this, i will be using Nmap (Network Mapper). It is a free open-source utility used for network exploration, management, and security auditing.

  
   ![image](https://github.com/user-attachments/assets/85191351-3895-4832-9835-f96aba0dceb6)


- In the screenshot above, i used the command line tool Nmap to scan the localhost (Kali VM).
- Now that i have generated some traffic, i will head over to Elastic to query for security events. To do this, i will click on the menu icon at the top-left and then click on the "Logs" tab under "Observability".
  
    ![image](https://github.com/user-attachments/assets/2df030e6-fd28-45a8-99e9-14d1dca51f5a)

- In the search bar, i will enter a search query to filter the logs. I will enter the query process.args: "nmap" ![image](https://github.com/user-attachments/assets/b62ce71c-c682-47ef-90c0-bdcfc10f8730)

- I can also click on the details of each event to view more details, such as the nmap command used in the Kali VM.

   ![image](https://github.com/user-attachments/assets/fe9d946b-b64d-4034-8e25-4586a26c8fb5)

- Next, i will create a dashboard to visualize the events. I will start by navigationg to the Elastic web portal and click on the menu icon at the top-left and under "Analytics" i will select Dashboards.

   ![image](https://github.com/user-attachments/assets/47029732-13c9-4294-a52e-acad3684121e)

- I will then select "Create dashboard" >  "Create Visualization" and then select "Area" as the visualization type. This will create a chart that shows the count of events over time.

   ![image](https://github.com/user-attachments/assets/f1af643f-c586-4e78-a045-b0ffc649261f)

- In the "Metrics" section of the visialization editor on the right, i'll select "Count" as the vertical field type and "Timestamp" for the horizontal field. This will show counts over time.

   ![image](https://github.com/user-attachments/assets/8e6fb02b-13ed-4ae4-85aa-f5a509d6ae10)

- Once i have entered my metrics for the dashboard, i'll click on save, and now my dashboard is configured.

   ![image](https://github.com/user-attachments/assets/1c4db961-15cc-4695-8126-4e95cf527991)

- Now, i will create an alert for my SIEM. alerts are created based on predefined rules or custom queries, and can be configured to trigger specific actions when certian conditions are met. For this lab, i will create an alert to detect Nmap scans, and configure them to notify me via Email when they are detected.

- I will start by navigating to the menu icon and under "Security" i will click on "Alerts" then click on "Manage rules" at the top-right.

   ![image](https://github.com/user-attachments/assets/634a779d-7a0e-459b-adf1-c16eeb79b429)

- From here, i will click on "Create new rule" and under the "Define rule" section, i will select "Custom query" option from the dropdown menu. I will define the query that will send an aleart to the SIEM. The following query will match all events with the action "nmap_scan". I will then set the severity score to High and leave a discription below so that others who use the SIEM will understand what is happening with the alert.

   ![image](https://github.com/user-attachments/assets/d6cbe64d-b4ff-4e8c-9d35-343a3814d03d)
   ![image](https://github.com/user-attachments/assets/7ed4f404-e782-49a6-9123-a2574f5b960c)


- In the "Actions" section, there are various actions you can take when the rule is triggered. I will choose to send an email notifiaction to alert me when this rule is triggered.

   ![image](https://github.com/user-attachments/assets/94493155-8c47-4142-b110-fffdeefc68c6)

- I will go ahead and save this rule and test it out by running an Nmap scan on the Kali machine.


   ![image](https://github.com/user-attachments/assets/9125bc3f-22f4-44e0-af26-5db5f2821630)

- Now, i will go and check my email to see if the SIEM has sent me a notification.

   ![image](https://github.com/user-attachments/assets/ab6395b5-23bc-47ca-8bd8-352446be9ed6)
- Aha! it worked! Alert detected.

## Conclusion

- In this project, i set up a home lab using Elastic SIEM and Kali VM. I forwarded data from the Kali VM to the SIWM using Elastic Beats agent, generated security events on the Kali VM using Nmap, and queried/analyzed the logs in the SIWM using the Elastic web interface. I also created a dashboard to visualize security events and then created an aleart to detect & notify me of the triggered rule. 



   


   


  







   




  

   





