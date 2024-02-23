## 1.	Star schema design

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/be226bea-f865-43d0-999b-cb47a4bd6473)

## 1.2	Explanation on your star schema 

a.	What are the fact and dimensions and why they are chosen
Dimensions:  
GROUP9_DPRODUCTION for PRODUCTION
GROUP9_DCLIENT for CLIENT
GROUP9_DTHEATRE for THEATRE
GROUP9_DTIME for TIME
GROUP9_DTrow for Trow

Fact:
Group9_FTicketPurchase for TicketPurchase

Please refer to the diagram for the star schema.  P#, Client#, THEATRE#, and TR# are retained as dimension nature keys. The surrogate keys for dimensions are GROUP9_P_ID, GROUP9_CLIENT_ID, GROUP9_THEATRE_ID, GROUP9_TROW_ID, and GROUP9_TIME_ID.  The PK for GROUP9_P_ID is GROUP9_DPRODUCTION. The PK is GROUP9_CLIENT_ID for GROUP9_DCLIENT. The PK is GROUP9_THEATRE_ID for GROUP9_DTHEATRE. The PK is GROUP9_TIME_ID for GROUP9_DTIME. The PK is GROUP9_TROW_ID for GROUP9_DTrow.  A composite key made up of GROUP9 P ID, GROUP9 CLIENT ID, GROUP9 THEATRE ID, GROUP9 TROW ID, and GROUP9 TIME ID is used for Group9_FTicketPurchase.  A FK referring to GROUP9_DPRODUCTION is GROUP9_P_ID; an FK referring to GROUP9_CLIENT_ID; an FK referring to GROUP9_DCLIENT; an FK referring to GROUP9_THEATRE_ID; an FK referring to GROUP9_DTIME; and an FK referring to GROUP9_TROW_ID.   

## b.	Why their attributes are chosen

PRODUCTION
P# :- A unique identifier for each production.
TITLE :- The title of the production.

CLIENT
Client :- A unique identifier for each client.
TITLE :- The title of the client.

THEATRE
THEATRE :- A unique identifier for each theatre.
NAME :- A unique name for each theatre.

TIME
D_DATE :- A unique date for each time.
Month :- A unique month for each time.
Year :- A unique year for each time.
Year :-
Trow
TR# :- A unique identifier for each theatre row.
RowName :- The name of the row.
RowType :- The type of row (e.g., Front, Middle, Rear).

TicketPurchase
GROUP9_P_ID :- A foreign key that references the production.
GROUP9_CLIENT_ID :- A foreign key that references the client.
GROUP9_THEATRE_ID :- A foreign key that references the theatre.
GROUP9_TIME_ID :- A foreign key that references the time.
GROUP9_TROW_ID :- A foreign key that references the trow.
TOTALAMOUNT :- The total amount of the ticket sale.

The MT Company's needs for managing reservations, ticketing, and data analysis of ticket sales are taken into consideration when selecting these qualities. This fact table's granularity of data includes specific descriptions for every aspect of the business, including theater locations, production details, and customer information, down to the level of individual ticket purchases.
c.	What is the granularity

The granularity, for each row in TicketPurchase, it represents the TOTALAMOUNT ticket purchase by one client for one theatre at one time in one row .

2.	Derivation of logical relations


2.1	A list of logical relations

GROUP9_DPRODUCTION (GROUP9_P_ID, P#, TITLE);
GROUP9_DCLIENT( GROUP9_CLIENT_ID, Client#, TITLE);
GROUP9_DTHEATRE (GROUP9_THEATRE_ID, THEATRE#,NAME);
GROUP9_DTIME(GROUP9_TIME_ID, D_DATE, Month, Year);
GROUP9_DTrow (GROUP9_TROW_ID, TR#, RowName, ROWTYPE);
Group9_FTicketPurchase (GROUP9_THEATRE_ID, GROUP9_CLIENT_ID, GROUP9_P_ID, GROUP9_TROW_ID, GROUP9_TIME_ID);




2.2	Explanation on the mapping from your star schema to the logical relations 

a.	How is the logical relations mapped from your star schema (which relations is corresponding to which entity in your star schema)
A star schema has dimension tables surrounding the fact table at its core. Keys to all of the dimension tables are included in the fact table. This is how the mapping functions:

Fact Table:- Group9_FTicketPurchase represents the transactions related to ticket sales. It has foreign keys that point to the dimension tables' primary keys.
Tables of Dimensions:-
 Group9_DTHEATRE is associated with the Theatre entity and contains information about theatre sites.
Group9_DCLIENT is a customer-related group that matches the Client entity. Group9_DPRODUCTION is the Production entity that contains information about theatrical productions.
Group9_DTrow is equivalent to the Trow entity, containing information about the names and types of rows in a theatre.
The Date_Dimension entity's Group9_DTIME contains information about the time and date.


b.	What are the Primary Keys (PK) and Foreign Keys (FK) in the fact and dimensions.  For each FK, what does it refer to ? 
Dimensions:-
For GROUP9 DPRODUCTION the PK is GROUP9_P_ID. 
For GROUP9 DCLIENT the PK is GROUP9_CLIENT_ID.
For GROUP9_DTHEATRE the PK is GROUP9_THEATRE_ID.
For GROUP9 DTIME the PK is GROUP9_TIME_ID.
For GROUP9 DTrow the PK is GROUP9_TROW_ID.

Fact:-
GROUP9_P_ID is FK in Group9_FTicketPurchase. 
GROUP9_CLIENT_ID is FK in Group9_FTicketPurchase.
GROUP9_THEATRE_ID is FK in Group9_FTicketPurchase.
GROUP9_TIME_ID is FK in Group9_FTicketPurchase.
GROUP9_TROW_ID is FK in Group9_FTicketPurchase.

The matching PK of a dimension table is joined with each FK in the fact table. This preserves the normalization of the fact table, with the descriptive data being contained in the dimension tables. Because the fact table has all the keys required to connect with the dimensions and get pertinent descriptive data, this design makes quick querying and reporting possible.

3.	Creation of tables with integrity rules


3.1	SQL code for each table creation
3.2	 Evidence of the code working and table created (small screenshots)


CREATE SEQUENCE GROUP9_DPRODUCTION_seq
 START WITH 1
 INCREMENT BY 1
 NOCACHE
 NOCYCLE;

CREATE TABLE GROUP9_DPRODUCTION (
 GROUP9_P_ID  Number(6)   PRIMARY KEY,
   P#  number(6) NOT NULL,
   TITLE varchar2 (25) NOT NULL


![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/2f229ef6-af0f-41ea-b56c-71dc719d1887)

## CREATE SEQUENCE GROUP9_DCLIENT_seq
 START WITH     1
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;

CREATE TABLE GROUP9_DCLIENT(
 GROUP9_CLIENT_ID  Number(6)  PRIMARY KEY,
   Client# number(6) NOT NULL,
   TITLE VARCHAR2 (4),
 NAME  Varchar2(25) NOT NULL );

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/37bbb069-5af0-4eae-9479-e4b3a192a86b)

CREATE SEQUENCE GROUP9_DTHEATRE_seq
 START WITH     1
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;

CREATE TABLE GROUP9_DTHEATRE (
GROUP9_THEATRE_ID  Number(6)  PRIMARY KEY,
    THEATRE# Number(6) NOT NULL, 
   NAME varchar2(25) NOT NULL
);

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/69213094-b1ce-4428-9c96-f54a9c692e3d)


CREATE SEQUENCE GROUP9_DTIME_seq
 START WITH     1
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;

CREATE TABLE GROUP9_DTIME(
  GROUP9_TIME_ID NUMBER(5) PRIMARY KEY,
     D_DATE Number(2) NOT NULL,
    Month VARCHAR2(2) NOT NULL,
    Year NUMBER(4) NOT NULL
);

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/3969968e-ace8-4976-be04-7967d2b1fe0d)

CREATE SEQUENCE GROUP9_DTrow_seq
 START WITH     1
 INCREMENT BY   1
 NOCACHE
 NOCYCLE;

CREATE TABLE GROUP9_DTrow (
 GROUP9_TROW_ID Number(6)  PRIMARY KEY,
TR# Number(6) NOT NULL,  
 RowName Varchar2(25) NOT NULL ,
ROWTYPE VARCHAR2 (25) NOT NULL
);

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/7dada6f4-d96d-4fa0-924c-ff1a8d736f98)

CREATE TABLE Group9_FTicketPurchase(
 GROUP9_THEATRE_ID Number(6)  CONSTRAINT A1 REFERENCES GROUP9_DTHEATRE,
 GROUP9_CLIENT_ID Number(6)   CONSTRAINT A2  REFERENCES GROUP9_DCLIENT,
GROUP9_P_ID  Number(6)  CONSTRAINT A3 REFERENCES GROUP9_DPRODUCTION,
GROUP9_TROW_ID    NUMBER(6)   CONSTRAINT A4 REFERENCES GROUP9_DTROW,
GROUP9_TIME_ID NUMBER(6)  CONSTRAINT A5 REFERENCES GROUP9_DTIME,
    TOTALAMOUNT NUMBER(15) NOT NULL,
  constraint A6 primary key (GROUP9_THEATRE_ID, GROUP9_CLIENT_ID, GROUP9_P_ID, GROUP9_TROW_ID, GROUP9_TIME_ID));


![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/11ed9011-6cc6-433e-b8d9-e3f0933ac3bb)

4.	Data source identification, data extraction, transformation and loading

4.1	Data source mapping
Please draw the map between data source and their destination in your Data Mart

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/42bfb29b-d143-4d63-9276-142d20b8058d)


![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/19a1a48c-c8e5-4422-b658-dc5931f9404f)

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/1929b889-8ecd-4e6e-b08e-82f9bfed97ab)

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/2c0f36dc-d380-4694-b032-71ec9c23957c)

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/ab35ab58-3f27-43e1-a2e5-dd8a7a2844fa)

For each ETL operation:
4.2	ETL code
4.3	Evidence of ETL code works
Please provide the screenshot to show your code works and give the correct result.  If the output is long, just show the last screen with the returned number of rows inserted.





insert into GROUP9_DPRODUCTION select GROUP9_DPRODUCTION_seq.nextval, P# ,TITLE from
(select distinct P# , upper(trim(TITLE))TITLE from 
(select  P.P#, P.TITLE
From ops$yyang00.production P, ops$yyang00.performance PF,ops$yyang00.ticketpurchase TP
where PF.P# = P.P#  and PF.Per# = TP.Per#));


![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/6427485f-af4c-4f60-b633-aa6dbc975441)



insert into GROUP9_DCLIENT select GROUP9_DCLIENT_seq.nextval, Client# ,TITLE,NAME from
(select distinct Client#, upper(trim(TITLE))TITLE,upper(trim( NAME)) Name from 
(select  C.Client#,C.TITLE,C.NAME
From ops$yyang00.client C,ops$yyang00.ticketpurchase TP
where TP.Client# = C.Client#));

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/0eb9d612-e6dc-4c8e-a27f-5c5ccdf20798)

insert into GROUP9_DTHEATRE select GROUP9_DTHEATRE_seq.nextval, THEATRE#, NAME from
(select distinct THEATRE#, upper(trim( NAME)) NAME  from
(select TH.THEATRE#,TH.NAME from 
 ops$yyang00.theatre TH,ops$yyang00.performance PF,ops$yyang00.ticketpurchase TP
where PF.THEATRE# = TH.THEATRE# and PF.Per# = TP.Per#));


![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/15e19460-f85b-41ed-a4c3-cb4a85f6df3b)

insert into GROUP9_DTIME select GROUP9_DTIME_seq.nextval, D_DATE, Month, Year from
(select distinct extract(DAY from pDate) D_DATE, extract(year from pDate) year,
extract(month from pDate) month from
  ops$yyang00.Performance);

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/7bea89a5-a40c-453f-b68c-bde4f725d766)

insert into GROUP9_DTrow select GROUP9_DTrow_seq.nextval,TR#,RowName,ROWTYPE from
(select distinct TR#,upper(trim(RowName))RowName,UPPER(TRIM(ROWTYPE))ROWTYPE from
(select TR.TR#, TR.RowName,TR.ROWTYPE 
from ops$yyang00.TRow TR,ops$yyang00.TSeat TS,ops$yyang00.ticketpurchase TP
where TR.TR# = TS.TR# and TS.TS# = TP.TS#));

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/b7e468c2-73cf-45ed-b40c-2174207dbfb2)

insert into Group9_FTicketpurchase

 select GROUP9_THEATRE_ID, GROUP9_CLIENT_ID,GROUP9_P_ID, GROUP9_TROW_ID, GROUP9_TIME_ID, TOTAL

  from (select DTH.GROUP9_THEATRE_ID ,DC.GROUP9_CLIENT_ID, DPRO.GROUP9_P_ID,DTr.GROUP9_TROW_ID,

 DT.GROUP9_time_id, sum(TOTALAMOUNT) TOTAL from GROUP9_DTHEATRE DTH, GROUP9_DCLIENT DC, GROUP9_DTrow DTR, GROUP9_DPRODUCTION DPRO, GROUP9_DTIME DT, 

 ops$yyang00.ticketpurchase tp, ops$yyang00.performance pF, ops$yyang00.tseat ts where ts.ts#=tp.ts# and DC.client#=tp.client# and pF.per#=tp.per# and

  DTH.theatre#=pF.theatre# and DTr.tr#=ts.tr# and DPRO.p#=pF.p# and extract(day from pF.pdate)=DT.d_DATE and 

  extract(month from pF.pdate)=DT.month and extract(year from pF.pdate)=DT.year group by DTH.GROUP9_theatre_id, 
DC.GROUP9_client_id, DTr.GROUP9_trow_id, DpRO.GROUP9_p_id, DT.GROUP9_time_id);

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/333e20e5-1327-4a9d-9518-3a75382af6a3)

select * from GROUP9_DPRODUCTION;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/16fd06d1-0c1e-470c-bb66-9afc04d3e067)

select * from GROUP9_DCLIENT;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/3a5b7e52-8972-49d9-92e8-eea3b9a7cce6)

select * from GROUP9_DTHEATRE;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/f52038d7-ce49-48db-a305-50e9913b5b2c)

select * from GROUP9_DTIME;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/58918277-6dc6-41cb-ae16-ee2c283eaba0)

select * from GROUP9_DTrow;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/8ebbba50-1616-4c5e-981e-0f1f275ad741)

select * from Group9_FTicketpurchase;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/0b609801-a464-4e8b-9d6c-ecaae8ae417d)

5.	Data analysis 
5.1	SQL code for the required queries (both Data Mart and the relational model)
5.2	Evidence of the SQL code working and their results
Please provide the screenshots for your execution of your code and their results.  If the result is too long, provide only the last screen.


Production-wise reporting of Daily Analysis:-
Relational Model:
select  pro.p#, pro.title, extract(day from pdate) day, extract(month from pdate)month,
extract(year from pdate)year,sum(totalamount) Sale
from ops$yyang00.production pro, ops$yyang00.performance pf, 
ops$yyang00.ticketpurchase tp where pf.per#=tp.per# and pro.p#=pf.p#
group by pro.p#, pro.title, 
extract(day from pdate), extract(month from pdate), extract(year from pdate);

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/ce854ba6-de8d-46a6-a7ee-b306764bbca0)

Data Mart:
select dpro.title, dpro.p# ,dt.d_date,dt.month,dt.year, sum(totalamount) 
from group9_dproduction dpro, group9_dtime dt, group9_fticketpurchase ftp
where dt.group9_time_id=ftp.group9_time_id and dpro.group9_p_id=ftp.group9_p_id
group by dpro.title, dpro.p# , dt.d_date, dt.month, dt.year;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/a3a79322-f39f-498b-9cdb-e193c9097aab)

The Title and Total Sale of each production:
Relational Model:
select pro.title, sum(totalamount) from 
ops$yyang00.production pro, ops$yyang00.ticketpurchase tp, ops$yyang00.performance pf
where pro.p#=pf.p# and tp.per#=pf.per# group by pro.title;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/b6f254ca-c23a-47a9-8638-f0c915b93b36)

Data Mart:
select dpro.title, sum(totalamount) from 
group9_dproduction dpro, group9_fticketpurchase ftp
where dpro.group9_p_id=ftp.group9_p_id group by dpro.title;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/fe525d68-799c-4fb6-a5da-44e05ea07746)

The theatre name and total yearly sale for each theatre:
Relational Model:
select th.name , extract(year from pdate)year, sum(totalamount)TotalSale 
from ops$yyang00.theatre th, ops$yyang00.performance pf, ops$yyang00.ticketpurchase tp
where th.theatre#=pf.theatre# and pf.per#=tp.per# group by
th.name, extract(year from pdate);

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/fabfc90f-64ae-42b4-9e30-398072a095b0)

Data Mart:
select dth.name, dt.year, sum(totalamount)total from
group9_dtheatre dth, group9_dtime dt, group9_fticketpurchase ftp
where dth.group9_theatre_id=ftp.group9_theatre_id
 and dt.group9_time_id=ftp.group9_time_id 
 group by dth.name, dt.year;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/569ae1a7-d90f-451c-a9aa-0cc5049d367e)


The clients visited MT in at least 6 different months in a year:
Relational Model:
select count( distinct extract(month from pdate))NumberOfMonths,
 extract(year from pdate) year,c.name
from ops$yyang00.client c, ops$yyang00.performance pf,
 ops$yyang00.ticketpurchase tp, ops$yyang00.theatre th
where c.client#=tp.client# and pf.per#=tp.per# and th.theatre#=pf.theatre#
 group by c.name, extract(year from pdate) having count(distinct extract(month from pdate))>=6

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/9d494916-b165-478d-9e20-288039e79a2e)


Data Mart:
select dc.name , dt.year, count(distinct dt.month)
  from group9_fticketpurchase ftp, group9_dclient dc, group9_dtime dt, group9_dtheatre dth
  where dt.group9_time_id=ftp.group9_time_id and dc.group9_client_id=ftp.group9_client_id
and dth.group9_theatre_id=ftp.group9_theatre_id
  group by dc.name, dt.year having count(distinct month) >=6;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/e54b286d-628b-4023-8c8c-ccbfd6c34509)

The number of clients who have only visited MT theatres in one single month and no visit in any other month:
Data Mart:
select count(dc.group9_client_id), dt.year, count(distinct month) from
group9_dtheatre dth, group9_dclient dc, 
   group9_dtime dt, group9_fticketpurchase ftp
   where dth.group9_theatre_id=ftp.group9_theatre_id 
   and dc.group9_client_id=ftp.group9_client_id
   and dt.group9_time_id=ftp.group9_time_id group by dc.group9_client_id, dt.year 
   having count(distinct dt.month)=1;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/7b4bffb9-2158-4047-8826-8a9eed1ca639)

Relational model:


The month of the year with the highest ticket sale for a theatre each year:
select extract(month from pf.pdate)month, extract(year from pf.pdate)year ,th.theatre# 
from ops$yyang00.theatre th, ops$yyang00.performance pf, ops$yyang00.ticketpurchase tp
where th.theatre#=pf.theatre# and pf.per#=tp.per# and
 totalamount=(select max(totalamount) from ops$yyang00.ticketpurchase tp1
  , ops$yyang00.performance pf1 where tp1.per#=pf1.per# and 
  extract(month from pf1.pdate)=extract(month from pf.pdate));

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/7032b730-edaa-48b4-b8c8-28923f5d2895)

Data Mart:
SELECT Theatre_Name, Year, Month, Total_Sales
FROM (
    SELECT 
        DTH.NAME Theatre_Name,
        DT.Year,
        DT.Month,
        SUM(FTP.TOTALAMOUNT) Total_Sales,
        RANK() OVER (PARTITION BY DTH.NAME, DT.Year ORDER BY SUM(FTP.TOTALAMOUNT) DESC) Sale_Rank
    FROM  GROUP9_DTHEATRE DTH,  GROUP9_DTIME DT,    GROUP9_FTICKETPURCHASE ftp
    where dth.group9_theatre_id=ftp.group9_theatre_id and dt.group9_time_id=ftp.group9_time_id 
    GROUP BY  DTH.NAME, DT.Year, DT.Month
) WHERE Sale_Rank = 1;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/015a8020-38bf-4c97-863f-78a3d3b2af27)

The most popular row type in each theatre by value of ticket sale:

Relational model:

select row_type, theatre_name , max(totalsale)max_sale 
from (select th.name theatre_name, tr.rowtype row_type,
sum(tp.totalamount)totalsale from
 ops$yyang00.theatre th, ops$yyang00.trow tr, ops$yyang00.ticketpurchase tp
 ,ops$yyang00.tseat ts, ops$yyang00.performance pf where
 th.theatre#=pf.theatre# and pf.per#=tp.per# and tr.tr#=ts.tr# 
 and ts.ts#=tp.ts# group by th.name,tr.rowtype ) group by row_type, theatre_name;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/5a156a64-2444-4e76-962c-57cb373194bc)

Data mart:
select theatre_name, row_type, max(totalsale)max_sale 
from (select dth.name theatre_name, dtr.rowtype row_type
, sum(ftp.totalamount)totalsale 
from group9_fticketpurchase ftp, group9_dtheatre dth, group9_dtrow dtr
where dth.group9_theatre_id=ftp.group9_theatre_id and 
dtr.group9_trow_id=ftp.group9_trow_id 
group by dth.name, dtr.rowtype) group by theatre_name, row_type;

![image](https://github.com/kireetigudla/Data_Warehouse_MT/assets/122108823/e4a7979b-a945-42b1-bda1-a6d9f5692ec5)

6.	Justification of the data mart design and comparison of data mart and OLTP

6.1	Please compare your solutions in 5 and comment on how they satisfy the requirements of the data analysis. Furthermore, please compare Data Mart and the relational model in data analysis in general. 

Ist requirement is satisfied as each row gives the the sale analysis of each production according to date.
2nd requirement is satisfied as the result in second query gives the total sale of both the given years according to each oduction.
3rd requirement is satisfied as the query gives the total yearly sale for each theatre with the theatre name.
4th requirement is satisfied as it gives those client names who have visited the theatres of MT in minimum of 6 different months in a year.
5th requirement is satisfied as the query gives the number of clients who have visited the theatres only in one month of the year ,they may have visited more than one time .

Comparing both data mart and relational model, although comprising data mart is difficult however running queried with data mart is simpler than relational model as while running queries in data mart it requires less join conditions and give accurate result as it categorises evreything and makes easy for users to analyse data easily.

7.	Critical analysis and reflection

7.1	Please give a critical analysis on your group’s work, what is your success, what is not as expected. How is your group collaboration.  With more time, what could be further improved.  The management evaluation report from each member will have impact on this part.

Our experience with the data warehouse project has been extremely educational and enriching. In addition to some significant achievements, our group has faced some challenges.
The first step was to realise the dimensions tables and fact one in our data warehouse model.
Working together as a group was crucial for exchanging ideas and supporting those in need. We collaborated to decide on a crucial next step: identifying which tables and attributes would be most helpful. We did run into a few issues with this section, though. Since it would direct the remainder of our work, this section was the most crucial. The 'Performance' table was initially intended to be used as a fact table. However, after closely examining the requirements for the data mart, we determined that the TicketPurchase table was the best fit because the requirements stated that the analysis of ticket sales was a crucial component. Therefore, the 'TicketPurchase' table served our purposes the best, especially because of the 'TotalAmount' attribute. This section aided in our comprehension of the case study's user requirements. Everyone contributed their skills to the project, which increased our efficiency even more due to the equitable distribution of tasks.
