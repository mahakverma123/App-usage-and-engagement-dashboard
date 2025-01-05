

# App usage and engagement dashboard

### Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiODExYzg4YzYtNjczMC00YzViLWJjNTctMzZlOTQ0NzE0OTllIiwidCI6ImYwZWNmMWMwLTdmMWQtNDRhZC04NjA1LTBkYWQ4YTI5NWU5ZCJ9

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
- Step 5 : Below mentioned visuals and KPIs were developed:

(a) Users used/not used app in video call: This visual shows how many users used the app during video calls. A new column was created using a DAX which identifies users who did not use the app.

      count_with_no_call_users = 'users with call and no call'[count_all_user]-'users with call and no call'[count_with_call_users]

  Snap of new columns,

 <img width="233" alt="User with call_no call"   src="https://github.com/user-attachments/assets/1a4fac1b-ba89-4c78-a5eb-b101b2f0f1de" />


(b) Score card(Overall,current release and last release): These card charts show video call and app session durations for the overall, current, and previous app versions. Durations (in seconds) were converted to Day:HH:M:S format using DAX, and another DAX formula calculates the total number of day since app was released.
     
     DAX for converting seconds to Day:HH:M:S format

    sum__totalcall_HHMMformat = 
    FORMAT(INT([Sum_total_call] / (24 * 60 * 60)), "0""Days:""") &
    FORMAT(INT(MOD([Sum_total_call] / (60 * 60), 24)), "0""h:""") &
    FORMAT(INT(MOD([Sum_total_call] / 60, 60)), "0""m""")

    DAX for calculate the total number of day since app was released:

    overall_release_active_status = DATEDIFF(DATE(2024, 04, 08),TODAY(), DAY)
  
(c) Session by date: This visual shows the number of app sessions initiated each day, with the X-axis showing dates and the Y-axis showing the session count.

(d) Percentage of users used/not used app in video call: This chart shows the percentage of users who used or didn’t use the app during video calls for each app version. The percentages were calculated using a DAX formula to create a new column.
     
      count_with_call_users % = DIVIDE('users with call and no call'[count_with_call_users],'users with call and no call'[count_all_user])*100

      count_with_no_call_users % = DIVIDE('users with call and no call'[count_with_no_call_users],'users with call and no call'[count_all_user])*100
      
  Snap of new columns,

  <img width="262" alt="Percentage of users used_not used app in video call" src="https://github.com/user-attachments/assets/7c28030d-98fb-4ee3-a3b3-4f6eee0f3f62" />

(e) Stickiness metrics: This  section includes a card showing the total daily(DAU), weekly(WAU), and monthly active users(MAU), a line chart displaying the DAU/MAU % trend for each month (calculated using DAX), and a gauge visual highlighting the overall DAU/MAU % and DAU/WAU %.

    DAU/MAU = DIVIDE(
	AVERAGE('endpoint_10_DAU_WAU'[list_report_15th.count_active]),
	AVERAGE('endpoint_10_MAU'[list_report_monthly.count_active]))*100

(f) NPS Overview: The NPS Overview chart displays the number of promoters, detractors, passives, and the NPS score for each version. NPS is calculated using DAX formulas: one for Promoter% and Detractor%, and another for NPS.
 
        Promoter % = DIVIDE(
    [Promoters Count],
    DISTINCTCOUNT('public nps_ratings'[Index])) * 100

    Detractor % = DIVIDE(
    [Detractors Count],
    DISTINCTCOUNT('public nps_ratings'[Index])) * 100

    NPS score = ROUND([Promoter %] - [Detractor %],0)

A tooltip page shows the weekly NPS trend, with the week number (starting from the version's release) on the axis and the NPS score at the end of each week. Cumulative weekly NPS is calculated using a custom DAX formula.   

     CumulativeNPS = VAR MaxWeek = MAX('public nps_ratings'[Week_number])
     VAR Promoters = 
    CALCULATE(
        COUNTROWS('public nps_ratings'),
        'public nps_ratings'[NPS] = "Promoters",
        'public nps_ratings'[Week_number] <= MaxWeek
    )
    VAR Detractors = 
    CALCULATE(
        COUNTROWS('public nps_ratings'),
        'public nps_ratings'[NPS] = "Detractors",
        'public nps_ratings'[Week_number] <= MaxWeek )
    VAR TotalResponses = 
    CALCULATE(
        COUNTROWS('public nps_ratings'),
        'public nps_ratings'[Week_number] <MaxWeek)
        RETURN 
    IF(
    TotalResponses = 0,
    BLANK(),
     DIVIDE((Promoters - Detractors) * 100, TotalResponses))

(g) Engagement rate:This shows the percentage of users who used the app at least once and at least twice during video calls for each version, these were calculated by creating the column with below DAX.
 
      ER_1 = DIVIDE('Endpoint_engagement rate'[at_least_1_call],[Total_calls])*100

      ER_2 = DIVIDE('Endpoint_engagement rate'[at_least_2_call],[Total_calls])*100

snap of new columns,

<img width="159" alt="Engagement rate" src="https://github.com/user-attachments/assets/dc8a77b9-5d8d-4f4b-8af5-c6aa8c632081" />
 
(h) App usage trends over days: This visual shows the number of users who used the app for doing video conferencing for 1, 2, 3, up to 30 days.

(i) Old & New recurring users:This stacked chart shows the percentage of recurring users (those who have used the app at least 3 times) and new users during a video call in a specific calendar week.

(j) App User Insights: The visual is a funnel chart showing the following user insights:Registered Users: Total users who signed up for the app,Total Users: Users actively using the app,Active Users: Users who have used the app in the last 2 weeks,Recurring Users: Users who have used the app at least 3 times and Power Users: Users who used the app 3+ times in the last week and had sessions over 30 minutes.

(k) Average call duration(sec): This visual shows the average duration(in seconds) of app usage in video conferences for each version.

(l) Users per platform: This is a pie chart showing number of users uing the application on two operating systems: mac and windows.

(m) Versions used in last two weeks: This is an area chart showing app versions used in the last two weeks, with the Y-axis representing the number of users using each version.

(n) User language: This visual shows the language users choose to operate the app.

(o) Total users per version:This visual represents the count of users using each version.

(p) Cohort question and answer: This line chart shows the percentage of positive responses for each question across different versions. A DAX formula calculates the percentages, and a slicer has been added which allows you to select specific questions.

      %_Would you pay for the current version of this app? = DIVIDE(CALCULATE(
    COUNTROWS('public yesno & public user(cohort)'),
    'public yesno & public user(cohort)'[answer] = "Yes",
    'public yesno & public user(cohort)'[question] = "Would you pay for the current version of this app?" ),CALCULATE(
    COUNTROWS('public yesno & public user(cohort)'),
    'public yesno & public user(cohort)'[question] = "Would you pay for the current version of this app?"  ))*100

(q) User session distribution:The visual shows the number of users by how many times they used the app: 1 time, 2 times, 3 times, or 4+ times, for all versions.

(r) Cohort(Crashlogs.users,NPS): The visual displays crash log counts, user numbers, and NPS scores for each app version. A slicer allows selecting specific versions.As all the Data was from different tables, relationship was made  using the app version column for these tables.

 - Step 6 : The report was then published to Power BI Service.
 
 
<img width="371" alt="publish" src="https://github.com/user-attachments/assets/25f09d94-5fb9-4386-8192-1db47bf35630" />

# Snapshot of Dashboard 

<img width="881" alt="dashboard" src="https://github.com/user-attachments/assets/31e7e074-a158-40a8-924a-2532a2212bd8" />
