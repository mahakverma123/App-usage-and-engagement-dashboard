# App usage and engagement dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/384d017e-e935-44dc-9e7d-1626c1a36de1/ReportSection
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

  (a) Users used/not used app in video call: This visual shows how many users used the app during video calls. A new column was created using a DAX which identifies users who did not use the app.

  count_with_no_call_users = 'users with call and no call'[count_all_user]-'users with call and no call'[count_with_call_users]

  Snap of new columns,
 <img width="233" alt="User with call_no call"   src="https://github.com/user-attachments/assets/1a4fac1b-ba89-4c78-a5eb-b101b2f0f1de" />
