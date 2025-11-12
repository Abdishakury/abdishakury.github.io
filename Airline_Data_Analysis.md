# Airline Data Analysis
 - Portfolio [Link](https://github.com/Abdishakury/Portfolio)
 - [Jupyter Notebook](https://github.com/Abdishakury/Airline_data_analysis/blob/master/Arline_Data_Analysis.ipynb)

<img width="1250" height="699" alt="image" src="https://github.com/user-attachments/assets/c6d74301-b600-413e-8566-2d3665631654" />

### PROBLEM STATEMENT 
In last month, Airline have seen the high numbers of dissatisfied passengers. 
Satisfaction of passengers are one of the concern of the airline. We are one of those airlines who focuses on both Business travellers and personal travellers and our majority of the customers are loyal customers.  
Overview of the airline data shows that, there are some Amenities of facilities with low rating or passengers were unhappy with, which is one of factors of dissatisfaction among the passengers. Although we have seen that our flights have high average 
departure and arrival delay time, I believe there are some outliers in that records, because at many time we cannot do much about that, for example: technical breakdown or any software glitch, but this happen very rare and take lots of time 
which impact on departure delay. In overview of airline data there are many small age passengers, we believe that for authentic rating passenger’s age should be 16 or more than 16.  
So, tell us at which place we need to improve our self so that passenger’s satisfaction 
will increase.

# ASSUMPTIONS
1. Rating 4 and 5 will be consider as a good rating and below 4 will be consider as neutral or improvement require and 2 or         below 2 will be consider as bad rating. 
2. Eco Plus Class is upgrade of Eco Class services.   
3. Pricing of the tickets are fair along all classes of the airline.  
4. Passengers age should be 16 or more than 16 for authentic rating.  
5. There are some outliers in Departure and arrival delay time records.
6. Staff Experience is not effecting on the Rating of the airline amenities.
7. ‘0’ rating will be consider as not rated or service not provided.  

# RESEARCH QUESTIONS 
1. How much delay in departure and arrival time effect the satisfaction of the passengers?
2. Airline amenities with ‘0’ rating where ‘0’ means no service provide, and impact on satisfaction.
3. Which are the airline amenities with low rating.
4. Which type of passengers and preferred class give low rating to the airline amenities.

# DATA ANALYSIS AND FINDINGS
## Departure and Arrival delay Impact 
<img width="859" height="455" alt="image" src="https://github.com/user-attachments/assets/4e575c91-9d96-4b87-9f9f-f36d412be2ff" />

<img width="862" height="461" alt="image" src="https://github.com/user-attachments/assets/28deb08b-3e47-4c05-9e25-95d1e297f4e5" />
Here, 2nd Graph show that delay in arrival specially after 5 minutes may lead to dissatisfaction of the passengers. On the other hand there is not significant change in departure delay.

<img width="627" height="430" alt="image" src="https://github.com/user-attachments/assets/a36074c7-7232-40b7-90a1-81201052e901" />

As we can see in this graph around 90% of Personal travellers are dissatisfied and on the other side Business travellers ratio is around 50-50. 

<img width="703" height="426" alt="image" src="https://github.com/user-attachments/assets/bb47c173-a8ab-4f68-89cc-12c4e27cd22f" />

Here, specially among the business travellers who are disloyal have high dissatisfaction compare to loyal customer.  

**Finding:** By the above data analysis we find that, delay in departure have not much impact on satisfaction of the passengers, but passengers who face delay in arrival are mostly dissatisfied Specially after 5 minutes of delay. It look like delay in arrival definitely impact on the satisfaction of the travellers, rest other factor will be consider.  

### Amenities with 0 rating (service may not available or not provided)
<img width="1066" height="578" alt="image" src="https://github.com/user-attachments/assets/cbb91bc4-184c-4b6f-b74b-d3e4aafe9dd1" />
<img width="1010" height="467" alt="image" src="https://github.com/user-attachments/assets/786676d8-a49e-469a-9716-2a0755904c53" />
In case of Business travellers most of them are look satisfied, it may because business travellers booked their tickets by the contact of agents, hence they do not face any difficulty whether Online booking service is available or not. But In case of Personal travellers scenario is different, here most of them report dissatisfaction, It may have a chance that no online booking service impact on there satisfaction rating.

<img width="1017" height="528" alt="image" src="https://github.com/user-attachments/assets/efcf41c7-a966-476e-94ff-bd68e537bd1b" />

**Findings:** By the above analysis, Mostly Business class passengers reported no Inflight wifi service, but it may not impact on their satisfaction decision, similar case in other preferred classes.¶ In other unavailable services like online booking and online boarding, it look like Personal travellers hold the high chance to get dissatisfied but unavailability of these services. 

### Airline Amenities with frequent rating equal to 3 or less than 3. 
<img width="1037" height="487" alt="image" src="https://github.com/user-attachments/assets/034e50f5-5851-4cf5-ba76-41854d13ef40" />
Here, For Inflight wifi service most of the passengers rate below 4. Other graph show that Whether it is business class or eco or eco plus most of the passengers give 2 and 3 rating, which is not a good rating. 

<img width="996" height="349" alt="image" src="https://github.com/user-attachments/assets/8703a0a2-1de7-4a1a-9afd-b7fded5ca964" />
Similar as Inflight wifi service rating, Ease of online booking have low rating score, mostly below 4. Although Business travellers mostly rate 2 and 3 but also there are sort of similar count of business travellers who rate 4, but in case of personal travellers mostly rate 2 and 3 followed by 1 rating which means there is definitely personal travellers face some issue with online booking.   

**Finding:** Inflight wifi service is really concerning because all of the preferred class report low rating of 2-3 which is not consider as good rating, also there are many passengers who report no wifi as well in above data analysis, which means at many 
place wifi service is not available yet and if wifi service is present it is not working well. 
And for online booking it look like business travellers are sort of neutral but personal travellers give low rating of 2 and 3, it may because many business travellers book their tickets through agencies and personal travellers mostly book by them self.

### Average rating to Amenities by Type of travellers and preferred class 
<img width="983" height="583" alt="image" src="https://github.com/user-attachments/assets/8354add4-10e2-49b8-9ff7-0cc2d2a2b21d" />
<img width="1074" height="701" alt="image" src="https://github.com/user-attachments/assets/82bb5500-d2fa-4a80-a48d-f357e2cb1c25" />
After take a view, there are some amenities to address like: Inflight wifi service which we already analyse, similarly we analysed online booking and other looks ok but Online boarding for personal travellers seems to be concerning. In online boarding personal travellers average rating was low. 

<img width="746" height="400" alt="image" src="https://github.com/user-attachments/assets/d1685adb-40df-4aad-a650-5d46afad6cf8" />
Business travellers give good rating to online boarding, on the other hand personal travellers give mostly 3 followed by 2 and 4, which is consider as neutral rating.  

**Findings:** Here, it look like business travellers are sort of positive with online boarding, but personal travellers report sort of neutral rating of 3 followed by 2 and 4. which is consider as ok ok condition of online boarding. In above analysis there are also some passengers who report no online boarding which show impact specially on personal travellers. It means first at many place there are no online boarding service, and if it is there then it may not work satisfactory. 

# CONCLUSION 
At the last of this data analysis we found that there are 4 kind of issue with the airline. Delay in arrival, Inflight wifi service, Ease of online booking, Online boarding service.

If we consider other factors constant, delay in arrival have definitely impact on satisfaction of the passengers specially when the delay is more than 5 minutes and those passengers who travel for personal reasons are mostly dissatisfied, So if flights 
will have more delays in arrival this will definitely become one of the reason of dissatisfaction among the passengers.

Now come to the other issues like Inflight wifi, Online booking and Online boarding. Some of the passengers report unavailability of these service and if these service were there then they are not working well, in case of wifi most of passengers gave rating of below 3 which is really concerning, similar case with online booking, many of the passengers reported No online booking, mostly personal travellers were there it may because many business travellers prefer to book there tickets through agencies, but personal travellers really do it with Website or other portals, and if the online booking service was there then it would not working well, thats why mostly personal travellers give low rating to online booking service. But in Online boarding, ratings were sort of neutral but average rating of personal travellers was lower side, but at some place passengers reported No online boarding service, mostly personal travellers reported this and these are some issues which could be the reason of dissatisfaction among the passengers. 

# SUGGESTIONS 

1. Try to reduce flight delays, make it under 5 minutes specially in arrival, this will definitely left a good impression on the    passengers, and showcase your punctuality.
2. Improvement required in Inflight wifi service, in terms or connectivity and speed, Also it may possible that many passengers     did not know about the service or how to avail that.
3. Improvement required in software related services like Online booking and online boarding, possibly airline using outdated       technology or need a upgradation, and also there is a possibility that there are some bugs in airline online booking and         online boarding software.  
