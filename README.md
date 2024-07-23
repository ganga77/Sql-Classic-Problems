Question 1: Consecutive Available Seats
Write an SQL query to report all the consecutive available seats in the cinema, where free =1 means the seat is available.

Solution:

Step1: Make lead and lag window functions and find the consequitive numbers

SEAT_ID	FREE	LD	LG
1	      1	    0	  1000
2	      0	    1	  1
3	      1	    1	  0
4	      1	    1	  1
5	      1	  1000	1

Step2: Now select only those numbers which are in lead and lag window functions.

-------------------------

Question 2: Find the Start and End Number of Continuous Ranges

Solution:

Step1: Make row_number window function and subtract it from the Id. Name it as SEQ
Step2: Now form a group and extract the minimum and maximum from each group.

LOG_ID	RN	SEQ
1	      1	  0
2	      2	  0
3	      3	  0
7	      4	  3
8	      5	  3
10	    6	  4

Result:

MINIMUM	MAXIMUM
1	        3
7	        8
10	      10

--------------------------

Question 3: Active Users
Active users are those who logged in to their accounts for five or more consecutive days. Write an SQL query to find the id and the name of active users.


Accounts table:                 Logins table:
+----+----------+               +----+------------+
| id | name     |               | id | login_date |
+----+----------+               +----+------------+
| 1  | Winston  |               | 7  | 2020-05-30 |
| 7  | Jonathan |               | 1  | 2020-05-30 |
+----+----------+               | 7  | 2020-05-31 |
                                | 7  | 2020-06-01 |
                                | 7  | 2020-06-02 |
                                | 7  | 2020-06-02 |
                                | 7  | 2020-06-03 |
                                | 1  | 2020-06-07 |
                                | 7  | 2020-06-10 |
                                +----+------------+
Solution:
Step1: FInd the dense_rank partiton by id order by login_date

ID	LOGIN_DATE	RN
1	2020-05-30	  1
1	2020-06-07	  2
7	2020-05-30	  1
7	2020-05-31	  2
7	2020-06-01	  3
7	2020-06-02	  4
7	2020-06-02	  4
7	2020-06-03	  5
7	2020-06-10	  6

Step 2: Select only that name from accounts table where rn>=5 (This means that id is loggedin for 5 consequitive days)

-----------

Question 4: Human Traffic of Stadium
Write an SQL query to display the records with three or more rows with consecutive id's, and the number of people is greater than or equal to 100 for each.

Solution:

Step1: Select the difference between id and row_number and name it as seq.
Step2: Then select those ids where count(seq) >=3

                                
