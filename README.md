![header](https://user-images.githubusercontent.com/100329223/179633826-dffbe874-5372-427c-b8c4-857bd98b2ea1.png)
# The Impact of Funding on Students Pursuing Higher Education 
## The Background into Investigating Secondary Education Attendance after High School
Academic success can be the framework to a young individuals whole future. Dreams of being an astronaut, doctor, or trades worker can inspire someone to work to the best of their abilities in order to achieve that goal. While school systems are very structured and provide strict educational programming, there are many factors that go into each students’ accomplishments. In this analysis, we will be using multiple sources to determine whether there are any significant relationships between a student choosing to seek higher education and high school district demographics, financial characteristics, and extra-curricular funding, specifically in Wisconsin.
### Reasoning and Importance of this Analysis
Attending school isn’t strictly about academics and acing every test. School is a time when children form habits, create relationships, set goals, and develop new passions. Providing the opportunities for each student is essential and can determine the future path they take. There are many impacting factors that go into budgetary needs. Our analysis will determine the amount of funding provided per student in academic departments verses extra activity departments in determining the child’s chances of pursuing secondary education. 

School Districts have a lot to take into account when it comes to finding a balance in funding academics, assisted programs, extra-curricular activities, and other budgetary needs. The National Center for Education Statistics states “Extracurricular activities provide a channel for reinforcing the lessons learned in the classroom, offering students the opportunity to apply academic skills in a real-world context, and are thus considered part of a well-rounded education.” Through much of their research, they were able to provide statistical backing based on data collected from US public schools. Other organizations, such as the National Federation of State High School Associations, have done research on the importance of funding these activities even though they only make up a small portion of the overall budgetary funding provided per student. The benefits of budget allocation to these programs not only boost the academic success of its students, but improve community standards and create well rounded individuals that will continue on to have positive impacts on society. 

When parents are considering schools, they not only take into account the success of academic ratings, but the additional activities and organizations it has to offer. With careful budget analysis, school can set themselves up for the most success and an opportunity for growth by attracting more students, creating a positive reputation, and providing resources for each student to thrive.
 
### Data Sources Used for Analysis
Data for this project was pulled from publicly available information sources through the Wisconsin Department of Public Instruction (DPI). In order to measure district income and overall spending levels, data from the Comparative Cost (https://dpi.wi.gov/sfs/statistical/cost-revenue/section-d) and Comparative Revenue (https://dpi.wi.gov/sfs/statistical/cost-revenue/comparative-revenue-member) reports were pulled. In order to specifically allow the team to examine extracurricular spending, which is not reported on a comparative basis at the district levels, it was also necessary to pull full reported budgetary data per district from the School Finance Reporting Portal (https://dpi.wi.gov/sfs/reporting/safr/budget/data-download). In order to add information on district achievements and outcomes, data was pulled from the School and District Report Cards (https://dpi.wi.gov/accountability/report-cards) and from Statewide Post-Secondary Enrollment dashboards (https://dpi.wi.gov/wisedash/about-data/postsecondary). While data from DPI does contain primary keys referencing districts individually, the integration of these varied data sources proved challenging on several levels, which are explained further in the section on analysis and exploration.

![image](https://user-images.githubusercontent.com/100329223/179616093-a332e5b9-e28f-4820-809b-dc30af90e528.png)
### Postgres Database on AWS Cloud

Postgres database is spun up on AWS RDS instance to store the data, generate dashboards and perform the analysis. The data is transformed, cleansed and inserted into this database using python scripts.

![image](https://user-images.githubusercontent.com/100485119/181933905-a0b68c93-b1c0-4218-bff9-89314a21b4a3.png)
![image](https://user-images.githubusercontent.com/100485119/181933916-cfd52901-8f94-4ff8-a4fc-ca0e9dd67486.png)
![image](https://user-images.githubusercontent.com/100485119/181933941-ac20e74f-2f75-42b4-bc74-47d22263db67.png)


### Technologies Used for Analysis
Throughout this project, there will be various technologies used in order to form our analysis, and create a dashboard that will easily communicate the results to school district personnel, parents, or other curious individuals on the importance of funding allocations roll in student pursing higher education. 
Python will be our main programming language to conduct our analysis. Jupyter Notebook, SQL Postgres, and Google Colab will be the interactive web tool we will use to create computational output and visualizations. Machine learning concepts will be used to predict the impact of all variables within the data, with a focus on budgetary allotment to extracurricular activities, and the chances of a student continuing their education following high school. Once we have collected all of our data, altered the content to our needs, and created visual representations, we will use Flask to create a dashboard that clearly displays our findings. Amazon web service (AWS) may be used in cloud computing solutions, database storage, and content delivery. 

Below is a brief outline of the machine learning approach we plan on taking to achieve the percent of the budget allotted to each student in each category or activity:

![learning_machine_outline](https://user-images.githubusercontent.com/100329223/179615531-3e59a72d-a969-4546-8c42-e6ea8cb83860.png)

### Initial Analysis and Data Exploration
Initial data examination and identification began with making choices on what and how to scrape from the DPI site. Publicly available data goes back more than twenty years, so it was necessary for the team to first narrow down the scope. While a recent two- to three-year scope was identified by the team as desirable to examine trends, the global pandemic had a significant effect on school district reporting and trends, so a decision was made to collect data from the 2017-18, 2018-19, 2019-20, 2020-21, and 2021-22 school years. In this way, the team hoped to focus on multiple year trends and the most recent data, while still allowing for anomalous data from the years affected most by the pandemic. 

Examination began by pulling all available data for each year, joining the tables to create tables that reflected the longitudinal data for each report in preparation for more detailed examination, database creation, and table joins and querying.

#### Confounding Factors and Solutions
##### Data Availability
While pulling data, the team immediately identified two confounding factors: post-secondary data has not yet been reported and uploaded to DPI for the 2021-22 school year, and school district report card data is not available for the 2019-20 school year. 
![NoRptCd2019](https://user-images.githubusercontent.com/100329223/183537902-c44e6a0d-88c0-46f8-8092-b3813598a22a.png)

##### Data Point Inconsistency
Individual fields within the collected data that purported to show the same data still contained inconsistencies. For example, one report may refer to district 14 as "Adams-Friendship Area" and another as "Adams Friendship Area Schools". Most reports also contained student enrollment data, but the data varied slightly due to the points in time when it was collected. Districts report enrollment on the third Friday of September, but post-secondary enrollment reporting is based on much more dyniamic sources of information. 

Other important outlier data included district types. Typical extracurricular spending increases at the secondary level. While most districts within the state are K-12 (meaning they serve students from kindergarten through twelfth grade), there are a number of other configurations. For example, the Big Foot Joint School District is a 9-12 only district, serving four separate K-8 districts as a consolidated high school. Although the students all flow up to the same secondary school district, each feeder district maintains it's own costs, revenues, and budgets. 

##### Data Size
In order to gather specific data on extracurricular program, which is coded as "Co-Curricular Activities" in Wisconsin school district financial reporting documents, the team needed to pull full budgetary details for each school district over each year. The State of Wisconsin makes all of this data available, but because the data includes every single coded expenditure for every district for the entire school year, each year is split into multiple files. When combining this data, the team needed to make multiple decisions in order to pare the data down. Initial attempts to join the tables led to creation of a database that was so large even Google CoLab was unable to parse it.
![datasizestruggle](https://user-images.githubusercontent.com/100329223/183538256-b59c6b46-1b5a-41c1-a2f7-3366e23b9d7e.png)

### Machine Learning
The data, once taken in, required some preprocessing to get it ready for machine learning.  This involved removing identifying columns and columns where there weas only one unique value throughout the data.  

<img width="1029" alt="drop_columns" src="https://user-images.githubusercontent.com/99457275/182747899-37d8edcf-b89d-47bd-8a1e-fdd93dc34db3.png">

The feature selection was done mostly in cleaning the data, as we, as a team, determined what data was worth considering.  We had determined that spending in other areas of school administration were not needed for this analysis.   The data was split using train_test_split to ensure a random sample. 

<img width="680" alt="train_test_split" src="https://user-images.githubusercontent.com/99457275/182747940-2c28e967-18a2-4efb-9094-d200fef88ee5.png">

Model choice was initially a struggle, which led to a switch part way through the project.  While we initially wanted to try a deep neural network, we found that it was the wrong choice.  With some advisement from the instruction team, we settled on Random Forests as our machine learning model.  While we were unable to find the “sweet spot” of spending, we were able to determine which factors were the most important for our data.  

<img width="639" alt="ranking_feature_importance" src="https://user-images.githubusercontent.com/99457275/182748057-fb98340e-c0cb-4d8a-ab1f-f19c04face7b.png">

Our accuracy in this model was based on MAE, MSE, and oob (Out of Bag) score.  The MAE and MSE were large, but we suspect that was due to the large numbers used in this analysis. 

<img width="455" alt="mae_mse" src="https://user-images.githubusercontent.com/99457275/182748019-0e0144c8-355d-495c-ae36-63aea52aa43c.png">

However, the oob score, which is recommended to be between 0.75 and 1.0, was very close to 1.0, suggesting a strong model without overfitting.

<img width="547" alt="oob_score" src="https://user-images.githubusercontent.com/99457275/182747991-0edff02a-ae62-4682-ac44-bd351b1fde02.png">





Below is an outline of what will be within our dashboard:
![image](https://user-images.githubusercontent.com/100329223/182133044-1ea27941-db19-43c1-a31e-9962b62d2011.png)


Tableau: https://public.tableau.com/app/profile/staci.stapleton/viz/Activity_Spending_Education/Dashboard1

### Conclusion
Once data had been cleaned and filtered down into a set usable with the resources we had available (limiting post-secondary data to only full sets by school and limiting spending and achievement data to only the 2017-18 school year), we were not able to pinpoint a “sweet spot” of extracurricular spending per student.  However use of the Random Forests model allowed the team to identify important factors.  The three most important factors were total revenue, number of students, and the percentage of economically disadvantaged students.  While "group count" showed in our model as an important factor, it is a direct subset of the number of students, so was excluded from our final analysis.  After reviewing the results and correlations shown within the model, it was clear that larger, more affluent school districts (those with higher student counts and higher levels of revenue per student) are best poised to spend highly on extracurricular activites. 

Several factors merit further analysis using resources not available to a student group. Revenue levels per student are particularly sticky in Wisconsin, given the implementation of revenue growth caps in 1993. Since then, school districts have been limited to increasing their revenues within specific areas to a specific percentage, unless they use a referendum. Arguments have been made that the growth cap has artificially frozen districts into spending models that are not reflective of their current makeup and structure (https://www.wpr.org/rising-referendums-school-funding-101). Further longitudinal dives into the specific revenue levels per student historically may shed light on whether districts that have seen dramatic changes in makeup since the 1993 freeze are able to adjust and provide the same levels of extracurricular spending allowed by districts that have remained unchanged.

Website: https://lalita-ponnapalli.github.io/HS_Baseball_Scholarships/ 

Slideshow: https://docs.google.com/presentation/d/189JNHJ9g3HW9iKQu1dxWl6iNW47X_uBXRPmDhJm5V3o/edit#slide=id.g13e27def9eb_0_0
