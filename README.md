# Atliq HR Analytics || Power BI

## Introduction and Objective

1. Introduction

 
 Objective

The primary objective of this analysis is to know the reasons of higher leaves taken by the employees also knowing the contributions of working mode like 
1.WFH% 
2.Sick Leave%
3.Attendance % monthly  


## Steps followed 

#### 1.Transforming the data in Power BI tool power query. 
#### 2.Converting the column level data to row level data so that we have employees attendence on the single column, which will be easy for the analysis.
#### 3. Adding calculated columns like MMM YY - For the starting of the month( e.g. for 11-Apr-22 it will show as Apr 22)
                  
    MMM YY = STARTOFMONTH('Final Data'[Date])
#### 4. Adding calculated columns as "SL count"
        SL Count = SWITCH(
        TRUE(),
        'Final Data'[Value]="SL",1,
        'Final Data'[Value]="HSL", 0.5,0) 
#### 5. Adding calc. column Week Number & day of week 
      WeekNo = "W " & WEEKNUM('Final Data'[Date]) 
      day of week = FORMAT( 'Final Data'[Date], "ddd")
#### 6. Adding a seperate table for adding our measures for the analysis
 
 1.   
        Attendace % = DIVIDE([Present Days],[Office Working days],0)
2. Present days - To calculate the employee present days, 
this can done on the basis of specific filtered condition i.e., when the employee is present his/her attendance marked as "P"
so, to calculate this in power BI as a measure we use the DAX function 
      
    Present Days = CALCULATE([Count],'Final Data'[Value] in {"P", "WFH"}) 
3. Sick Leave Count:
     
        SL Count = SUM('Final Data'[SL Count])

4. SL% (Sick Leave %age) :

        SL % = DIVIDE('Measures (2)'[SL Count], [Office Working days])
5. WFH(Work from home) count 
          
       WFH Count = SUM('Final Data'[WFH Count])
6. WFH% 
      
        WFH % = DIVIDE([WFH Count],'Measures (2)'[Present Days],0)


Insights:

  1.Attendace is in decreasing trends.

  2.Sick leaves is in increasing treading as we move towrads the peak summer seasons.

  3.WFH% is on the increasing trend, employees are more likely to do the WFH.

  4. In a week higher presence is on the Monday - 93.2% and as we going down the week it was seen lowest presence in on the friday's and their will highsurge in WFH on specifically on friday's it means employees were more preffered to do WFH on friday specifically.

  ![BI File](https://github.com/user-attachments/assets/53537484-0b60-45bf-a6d1-9a3c7c3fe7c6)



