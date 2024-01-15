# Splunk

Completed Splunk4Rookies Workshop (hosted by Splunk) on 01/11/24

---

### Tools/Skills: 

Splunk - adding an app, exploring/searching data, creating dashboards, extracting fields

---

## LOGIN TO INSTANCE

Splunk provided an instance for each individual the attended the workshop. With the account info provided, I logged into mine.

## ADD NEW APP

I created an app within the instance for the use case of today's lesson. It's where I chose what data I wanted to monitor and created a dashboard based on specific searches.

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 9.53.20 AM.jpg" alt=""><figcaption></figcaption></figure>

## ADD DATA

The application is configured to collected weblogs into the splunk4rookies app I just created.

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 9.57.32 AM.jpg" alt=""><figcaption></figcaption></figure>

## EXPLORE DATA

In the workshop, there were several specific searches to perform to practice searching the data. After this practice, there were two challenge tasks to try. These are the challenge tasks and my answers to them.

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.11.03 AM.jpg" alt="" width="563"><figcaption></figcaption></figure>

</div>

### Q1 ANSWER

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.11.20 AM.jpg" alt=""><figcaption><p>Events with a status of 200 (successful) that are not purchase events</p></figcaption></figure>

### Q2 ANSWER

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.16.27 AM.jpg" alt=""><figcaption><p>Events with errors when trying to add or remove an item from the cart</p></figcaption></figure>

## CREATE DASHBOARD PANEL: WEBSITE SUCCESSES/FAILURES

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.17.24 AM (1).jpg" alt=""><figcaption></figcaption></figure>

</div>

I narrowed the search by specifying I'd like the data organized by time and separated based on the 10 most common status codes (count by status limit = 10).

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.20.21 AM.jpg" alt=""><figcaption></figcaption></figure>

After creating the dashboard panel, I added it to a new dashboard, "Buttercup Enterprise." I set it as absolute control, which allowed me complete control to configure how to dashboard is setup.

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.25.48 AM.jpg" alt="" width="375"><figcaption></figcaption></figure>

</div>

## CREATE DASHBOARD PANEL: CUSTOMER OS's

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.50.13 AM.jpg" alt=""><figcaption></figcaption></figure>

I perfomed a basic query on events within the last 60 minutes. From one of the events, I extracted the OS field and saved it as "platform". This would allow me to sort and query data based on what platform a user was utilizing.

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.51.19 AM.jpg" alt="" width="563"><figcaption></figcaption></figure>

</div>

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.54.14 AM.jpg" alt=""><figcaption></figcaption></figure>

</div>

I performed a search to create a dashboard for the most popular operating systems using the web app. Then, I saved this as a panel to the existing dashboard.

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 10.58.13 AM.jpg" alt="" width="375"><figcaption></figcaption></figure>

</div>

## CREATE DASHBOARD PANEL: BROWSERS WITH THE MOST FAILURES

The search for the browsers with the most failures, specifies that I only want to see failure (status>=400) and that I would like it to be organized by the top 5 browser types (useragent, limit) within time (timechart).&#x20;

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.02.06 AM.jpg" alt=""><figcaption></figcaption></figure>

Once created, I saved this panel to the existing dashboard, "Buttercup Enterprise."

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.02.19 AM.jpg" alt="" width="375"><figcaption></figcaption></figure>

</div>

## CREATE DASHBOARD PANEL: LOST REVENUE

<div align="center">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.15.09 AM.jpg" alt=""><figcaption></figcaption></figure>

</div>

I started with a basic lookup of the table product\_codes.csv to see what it looked like.

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.09.04 AM.jpg" alt=""><figcaption></figcaption></figure>

I then created a search that looked for purchase (action=purchase) failures (status>=400). I then cross queried the table product\_codes.csv. This table shared the product\_id column with the log data. By temporarily merging these tables on this column, I could ask the search to calculate the sum of the product\_prices that were part of the purchase failures. This information gives some insight into the revenue that could be lost from failures.&#x20;

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.13.33 AM (2).jpg" alt="" width="563"><figcaption></figcaption></figure>

</div>

I saved this panel to the existing dashboard.

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.14.41 AM (1).jpg" alt="" width="375"><figcaption></figcaption></figure>

</div>

## DASHBOARD PANEL: WEBSITE ACTIVITY BY LOCATION

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.24.37 AM.jpg" alt=""><figcaption></figcaption></figure>

I performed a search of where the web activity is coming from. I did this by using iplocation to match the clients' ip addresses to their location and then using geostats to count how many are in each city. I used a cluster map to visualize this.

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.28.12 AM (1).jpg" alt=""><figcaption></figcaption></figure>

I saved this panel to the existing dashboard.

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.29.07 AM.jpg" alt="" width="375"><figcaption></figcaption></figure>

</div>

### CHALLENGE: CREATE A MAP EXCLUDING THE U.S.A.

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.32.19 AM.jpg" alt=""><figcaption></figcaption></figure>

The challenge question asked me to update the search to remove the United States. I added in a line that specifically said the Country shouldn't be United States. I added this after I called on the iplocation so that the program had the information to sort out the US locations. I also specified search at the beginning of the argument because any search that happens after the main query in the beginning needs to be specified as a "search".&#x20;

### CHALLENGE ANSWER

<div align="left" data-full-width="false">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.32.30 AM (1).jpg" alt=""><figcaption></figcaption></figure>

</div>

## FINAL DASHBOARD

The final dashboard was easy enough to arrange. I imported a background that was recommended by the Splunk workshop instructor. I moved the various panels to where they were recommended to be. I made each panel transparent. I also got rid of some of the keys/legends that weren't necessary.

<div align="left">

<figure><img src=".gitbook/assets/Screenshot 2024-01-11 at 11.56.25 AM.jpg" alt="" width="563"><figcaption></figcaption></figure>

</div>

## Summary

In the end, I learned a lot in this workshop. I learned how to go from having an instance to creating an app (or apps) based on specific data in that instance and performing and saving queries as panels to a dashboard. I then learned how to reconfigure the dashboard so that it is even easier to read and work with.
