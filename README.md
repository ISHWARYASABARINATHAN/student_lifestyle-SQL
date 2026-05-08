**Project Title**
Student Lifestyle Analysis using SQL
**Objective**
The objective of this project is to analyze student lifestylepatterns to understand how different factors such as study hours,Sleep duration,Screen time,Physical Activity,Attendance and stress level affect student performance and overall well-being.

**This project helps to identify:**
- Productivity patterns among students
- Factors affecting academic performance
- Lifestyle habits influencing stress and health
- Relationship between Study time and grades

  **Dataset used**
  Student Lifestyle Dataset


**View Entire Dataset**
select * from student_lifestyle_dataset;

**1. What is the average study time of students?**
SELECT 
    AVG(Study_Hours_Per_Day) AS Average_Study_Time
FROM student_lifestyle_dataset;

**2. Which students have the highest academic performance?**
select Student_ID,
	GPA 
		from student_lifestyle_dataset
			where GPA = (select max(GPA) 
            from student_lifestyle_dataset);

**3. How does sleep duration affect GPA?**
select 
	case
		when  Sleep_Hours_Per_Day < 5 then 'Poor Sleep'
        when Sleep_Hours_Per_Day between 6 and 7 then 'Average Sleep'
        else
        'Healthy Sleep'
        end as Sleep_Category,
        avg(GPA) as Average_GPA
from student_lifestyle_dataset
group by Sleep_Category;

**4. What is the relationship between screen time and stress levels?**
select 
Stress_Level,
avg(Social_Hours_Per_Day) as Avg_Screen_Time
from student_lifestyle_dataset
group by Stress_Level
order by Avg_Screen_Time desc;

**5. Which studentsw maintain good attendance?**
select
	Student_ID,
    GPA,
    Sleep_Hours_Per_Day,
    Study_Hours_Per_day
    from student_lifestyle_dataset
    where GPA > 8
    and Sleep_Hours_Per_Day >=7
    and Study_Hours_Per_Day between 3 and 6;

**6. How many Student fall under different stress categories?**
select Stress_Level,
count(*) as Total_Students
from student_lifestyle_dataset
group by Stress_Level;

**7. Does physical activity improve academic performance?**
select 
case
when Physical_Activity_Hours_Per_Day < 1 then 'Low Activity'
when Physical_Activity_Hours_Per_Day between 1 and 3 then 'Moderate Activity'
else 'High Activity'
end as Activity_Category,
avg(GPA) as Average_GPA
from student_lifestyle_dataset
group by Activity_Category;

**8. What are the top factors affecting student lifestyle balance**
select
    avg(Study_Hours_Per_Day) as Avg_Study_Hours,
    avg(Sleep_Hours_Per_Day) as Avg_Sleep_Hours,
    avg(Social_Hours_Per_Day) as Avg_Social_Hours,
    avg(Physical_Activity_Hours_Per_Day) as Avg_Physical_Activity,
    avg(Extracurricular_Hours_Per_Day) as Avg_Extracurricular_Hours,
    avg(GPA) as Avg_GPA
    from student_lifestyle_dataset;

**9. Which students have unhealthy lifestyle patterns?**
select Student_ID,
Sleep_Hours_Per_Day,
Social_Hours_Per_Day,
Physical_Activity_Hours_Per_Day,
Stress_Level,
GPA 
from student_lifestyle_dataset
where Sleep_Hours_Per_Day < 5
and Social_Hours_Per_Day > 5
and Physical_Activity_Hours_Per_Day < 1 
and Stress_Level = 'High';

**10. Which Student have healthy or unhealthy fifestyle patterns based on sleep,screeb time, and physical activity?**
select
Student_ID,    
case
when Sleep_Hours_Per_Day < 5 then 'Poor Sleep'
else 'Healthy Sleep'
end as Sleep_Status,
case
when Social_Hours_Per_Day > 5 then 'High Screen Time'
else 'Controlled Screen Time'
end as  Screen_Time_Status,
case
when Physical_Activity_Hours_Per_Day < 1 then 'Low Activity'
else 'Active'
end as Activity_Status,
Stress_Level,
GPA

FROM student_lifestyle_dataset;

**Key Insights**
- Students with balanced sleep and study hours tend to perform better academically.
- Higher screen time is associated with increased stress levels.
- Students involved in regular physical activity generally show better focus and performance.
- Poor attendance often leads to lower academic scores.
- Excessive social media usage negatively impacts productivity.
- Healthy lifestyle habits contribute to improved student well-being and academic success.
