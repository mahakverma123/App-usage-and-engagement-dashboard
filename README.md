

# App usage and engagement dashboard

### Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiM2MzNThhNjQtMmEyMy00MDEyLWEwYjYtN2MwNjA2MjI2YTQ4IiwidCI6ImYwZWNmMWMwLTdmMWQtNDRhZC04NjA1LTBkYWQ4YTI5NWU5ZCJ9
## Introduction
VisionX is a cutting-edge application designed to seamlessly integrate with other popular video conferencing platforms, providing a significant enhancement to video and audio quality during virtual meetings. With the growing importance of clear communication in remote environments, VisionX leverages advanced algorithms and technologies to optimize video clarity, reduce lag, and ensure a smooth, uninterrupted experience for users.The app is available in two languages, English and German.

## Problem Statement
 To ensure the app's effectiveness and continuous improvement, the following key objectives need to be addressed:

1.User Feedback and Engagement: Understanding user satisfaction and engagement is essential to improve the app's usability and value.

2.Application Performance: Monitoring the app's performance across different scenarios is critical to ensure that it consistently delivers the promised video quality enhancements. 

3.Version Improvement Tracking: As VisionX evolves through multiple versions, it's essential to evaluate whether each new release brings tangible improvements.

These objectives have been addressed by presenting key insights and performance metrics based on the usage and impact of VisionX, helping to track its effectiveness and user satisfaction.

### Steps followed 

- Step 1 : The data stored in PostgreSQL is directly connected to Power BI
- Step 2 : Open power query editor & in view tab under Data preview section, check data types of columns and some of the columns with number where uploaded with data type as text so data type of these columns were changed to number or decimal.
- Step 3 : Based on the requirements, some data modelling was done by navigating to model view tab.
- Step 4 : Once all the data was loaded and data modelling was done successfully, KPIs and performane metrics were decided.
- Step 5 : Below mentioned metricsa nd KPIs were developed:

(a) Session by date: This visual shows the number of app sessions initiated each day, with the X-axis showing dates and the Y-axis showing the session count.
  
(b) Users used/not used app in video call: This visual shows how many users used the app during video calls. A new column was created using a DAX which identifies users who did not use the app.

      count_with_no_call_users = 'users with call and no call'[count_all_user]-'users with call and no call'[count_with_call_users]

  Snap of new columns,

 <img width="233" alt="User with call_no call"   src="https://github.com/user-attachments/assets/1a4fac1b-ba89-4c78-a5eb-b101b2f0f1de" />
  
(c) App usage trends over days: This visual shows the number of users who used the app for doing video conferencing for 1, 2, 3, up to 30 days.

(d) Percentage of users used/not used app in video call: This chart shows the percentage of users who used or didn’t use the app during video calls for each app version. The percentages were calculated using a DAX formula to create a new column.
     
      count_with_call_users % = DIVIDE('users with call and no call'[count_with_call_users],'users with call and no call'[count_all_user])*100

      count_with_no_call_users % = DIVIDE('users with call and no call'[count_with_no_call_users],'users with call and no call'[count_all_user])*100
      
  Snap of new columns,

  <img width="262" alt="Percentage of users used_not used app in video call" src="https://github.com/user-attachments/assets/7c28030d-98fb-4ee3-a3b3-4f6eee0f3f62" />

(e) Old & New recurring users:This stacked chart shows the percentage of recurring users (those who have used the app at least 3 times) and new users during a video call in a specific calendar week.

(f) App User Insights: The visual is a funnel chart showing the following user insights:Registered Users: Total users who signed up for the app,Total Users: Users actively using the app,Active Users: Users who have used the app in the last 2 weeks,Recurring Users: Users who have used the app at least 3 times and Power Users: Users who used the app 3+ times in the last week and had sessions over 30 minutes.

(g) Average call duration(sec): This visual shows the average duration(in seconds) of app usage in video conferences for each version.

(h) Users per platform: This is a pie chart showing number of users uing the application on two operating systems: mac and windows.

(i) Versions used in last two weeks: This is an area chart showing app versions used in the last two weeks, with the Y-axis representing the number of users using each version.

(j) User language: This visual shows the language users choose to operate the app.

(k) Total users per version:This visual represents the count of users using each version.

(l) Engagement rate:This shows the percentage of users who used the app at least once and at least twice during video calls for each version, these were calculated by creating the column with below DAX.
 
      ER_1 = DIVIDE('Endpoint_engagement rate'[at_least_1_call],[Total_calls])*100

      ER_2 = DIVIDE('Endpoint_engagement rate'[at_least_2_call],[Total_calls])*100

snap of new columns,

<img width="159" alt="Engagement rate" src="https://github.com/user-attachments/assets/dc8a77b9-5d8d-4f4b-8af5-c6aa8c632081" />
