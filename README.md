# social-media-addiction
# social-media-addiction
PURPOSE

 Its purpose is to help visualize and track how students are interacting with social media
 and how that usage may be impacting their mental health and well‑being.
 


 
 Here's a breakdown of the key components:
Top KPI Cards: Show total number of students affected, aggregate mental health score (or count of impacted students), and combined average daily usage hours.

Gender Filter: 

Allows toggling between Male and Female populations to compare behaviors and impacts.



Platform Usage Trend:  

A line chart showing total average daily usage hours by the most-used social media platforms—highlighting which platforms dominate student usage (e.g., Instagram, TikTok).

Geographic Insights:   

A bar chart titled “Top N by Country” (with a “Top 5” filter applied) showing which countries have the highest numbers of students affected or highest usage levels (e.g., USA, Spain, India).

Interactive Filters:  

Controls like Type (e.g., Default, Top 10, Top 5, Top 50) and gender selection to dynamically slice the data.


DAX Formula



1.TOTAL AFFECTED  

total_affected = sum('Students Social Media Addiction'[Addicted_Score])


2.RANKTABLE  

RankTable = DATATABLE("sort",INTEGER,"Type",STRING,"no",INTEGER,{
{0,"Default",0},
{1,"Top 5",5},
{2,"Top 10",10},
{3,"TOp 50",50}
}
)


3.TOPN  

var rankvalue = RANKX(ALL('Students Social Media Addiction'[Country]),[total_affected],,DESC)
 var selected_rank = SELECTEDVALUE(RankTable[no])
 RETURN
IF(selected_rank=0,[total_affected],
IF(rankvalue<=selected_rank,[total_affected],BLANK())
)
