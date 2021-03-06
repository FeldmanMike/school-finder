# Can Chicago Teachers Afford to Live Where They Teach?
Analyzing teacher salaries and nearby property values for Chicago Public Schools

LauraMargaret Burbach, Jonathan Rockower, Mike Feldman

See [here](https://github.com/FeldmanMike/school-finder/blob/master/burbach-jrockower-mikefeldman.pdf) for more detailed explanation of application

### How to Run School Finder Application
1. Install Python3.7 from source:
    https://linuxize.com/post/how-to-install-python-3-7-on-ubuntu-18-04/
2. Run install shell script
    `$ ./install.sh`
3. Enter virtual environment
    `$ source env/bin/activate`
4. Open data/school_codes.csv
    `$ subl data/school_codes.csv`
5. Run main.py
   ` $ python3.7 main.py [-a]`
      Optional `[-a]` parameter can be used to pull from archived versions of
      files without pulling via API. Without `[-a]`, the application takes us
      about 30 seconds to run.

### Files
1. `README.txt`
2. `requirements.txt`
3. `install.sh`
4. `socrata_request.py`
5. `assessors_request.py`
6. `cps_request.py`
7. `school_class.py`
8. `main.py`

### Project Goals and Accomplishments
Our project set out to answer the question: Can Chicago Public Schools teachers afford to buy homes near the schools where they teach?

The impetus for this work was the October 2019 Chicago Teachers Union strike, particularly the Union’s ask for teacher and staff raises in response to the rising cost of living. Much of the existing research on property values and schools is directed at parents looking at school attendance zones. We wanted to reframe property analyses from a teacher perspective, considering locations close to the school, but irrespective of attendance boundaries.

As the teacher workforce continues to become younger and less experienced nationwide, we wanted to look specifically at home-buying opportunities within 5 miles of a school. Home ownership, rather than renting, would signal stability and community investment. Real estate and budgeting websites cite a rule of thumb that buyers can afford a house priced at about 2 – 2.5 times their household income.

Our project addresses this question by providing an interactive tool that allows users to select a school and set a distance to see how teacher salaries at that school and sale prices around that school compare to those of all Chicago Public Schools teachers and all Cook County homes.

### Data Selection Notes
##### Assessor Data
1. Keep sales >= $10000
2. Remove observations with NaN values in both 'apts' (number of apartments) and 'n_units' (number of units within condominium complex) because it is unclear what type of properties these are
3. Set observations with '0' apts equal to '1' and those with negative apts to the absolute value of apts
4. Keep observations where 'most_recent_sale' == 1 to keep the most recent sale on a property
5. Remove 30,000 additional duplicates on 'pin' by keeping the most recent 'sale_date' observation for each 'pin'
6. Keep single family home and condominiums only to analyze data on sales of individual properties, not apartment buildings

##### Teacher Salary Data
1. Keep full-time employees
2. Keep people with job title: (a) Includes the word 'Teacher'; (b) Doesn't include the words: 'Assistant', 'Asst', 'Specialist', 'Analyst', 'Recruitment', 'Part-Time'
3. Filter out teachers who are not linked (through their Finance ID) to a specific school/school ID (approximately 600 observations dropped)
