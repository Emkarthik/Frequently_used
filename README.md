# Frequently_used


ping 202.83.21.12 -t

139.59.15.90

 C:\Program Files\PostgreSQL\9.6\bin\pg_dump -h 139.59.15.90 -U postgres --format=c -d talentify > db16nov.dump
 pg_restore -v -U postgres -d talentify C:\Users\Sumanth-Istar\Desktop\local25sept17.dump

FamilyShield OpenDNS server addresses
208.67.222.123
208.67.220.123


root@elt:~/apache-tomcat-9.0.0.M21/logs# tail -f catalina.out

OPEN DNS SERVER

208.67.222.222
208.67.220.220


Globle DNS


 DNS Provider 	 Primary DNS 	 Secondary DNS 
Google	            8.8.8.8	       8.8.4.4
Level3	          209.244.0.3 	 209.244.0.4
FreeDNS	         37.235.1.174	 37.235.1.177
ViperDNS	     208.76.50.50	 208.76.51.51


********restart**************

root@elt:~# ps -ef | grep java
root@elt:~# cd apache-tomcat-9.0.0.M21/
bin/     conf/    lib/     logs/    temp/    webapps/ work/
root@elt:~# cd apache-tomcat-9.0.0.M21/
root@elt:~/apache-tomcat-9.0.0.M21# cd bin/
root@elt:~/apache-tomcat-9.0.0.M21/bin# ./startup.sh





***************database dump***************************
DB BACKUP AND RESTORE CMD 
pg_dump -h localhost -p 5432 -U postgres -F c -b -v -f "/usr/local/backup/10.70.0.61.backup" old_db
pg_restore -h localhost -p 5432 -U postgres -d old_db -v "/usr/local/backup/10.70.0.61.backup" 
CREATE EXTENSION pgcrypto; 

*******************************************************

*************************For LOOP********************
package com.lessonxmlgenerator;

public class MAIN {
	 

	public static void main(String[] args)  {
		String str= "10564 ,10519 ,10524 ,10565 ,10567 ,10569 ,10520 ,10521 ,10525 ,10526 ,10527 ,10347 ,10523 ,10530 ,10381 ,10345 ,10350 ,10371 ,10379 ,10348 ,10382 ,10372 ,10355 ,10366 ,10364 ,10375 ,10356 ,10368 ,10358 ,10378 ,10346 ,10359 ,10362 ,10380 ,10363 ,10353 ,10352 ,10361 ,10369 ,10349 ,10354 ,10360 ,10370 ,10351 ,10377 ,10376 ,10373 ,10310 ,10385 ,10374 ,10367 ,10290 ,10544 ,10547 ,10357 ,10522 ,10365";
		String[] strs= str.split(",");
		for(String s : strs){
			String sql= "INSERT INTO task ( 	ID, 	NAME, 	description, 	task_type, 	priority, 	OWNER, 	actor, 	STATE, 	parent_task, 	start_date, 	end_date, 	duration_in_hours, 	assignee_team, 	assignee_member, 	is_repeatative, 	followup_date, 	is_active, 	tags, 	created_at, 	updated_at, 	item_id, 	item_type, 	project_id, 	is_timed_task, 	follow_up_duration_in_days ) VALUES 	( 		COALESCE ( 			(SELECT MAX(ID) + 1 FROM task), 			0 		), 		'Feedback Form', 		'Feedback Form', 		NULL, 		NULL, 		'300', 		"+s+", 		'SCHEDULED', 		NULL, 		'2017-12-03 0:01:00', 		'2017-12-05 23:59:59', 		NULL, 		NULL, 		NULL, 		NULL, 		NULL, 		't', 		NULL, 		now(), 		now(), 		'100', 		'CUSTOM_TASK', 		NULL, 		NULL, 		NULL 	);";
			System.out.println(sql);
		}
		
	}

}
*************************************************************************************************************************************************




************TO CREATE TRAINER_PRESENTOR********************


INSERT INTO istar_user (
	ID,
	email,
	PASSWORD,
	created_at,
	mobile,
	auth_token,
	login_type,
	is_verified
)
VALUES
	(
		(
			SELECT
				MAX (ID) + 1
			FROM
				istar_user
		),
		'shubhada.vaidyanath_presentor@gmail.com',
		'test123',
		now(),
		9999999999,
		'',
		NULL,
		't'
	);

	
	**************MAPPING TRAINER WITH A PRESENTOR*****************

INSERT INTO trainer_presentor (ID, trainer_id, presentor_id)
VALUES
	(
		(
			SELECT
				MAX (ID) + 1
			FROM
				trainer_presentor
		),
		2641,
		7749
	);
	**********************************************************************************************************
	
	
	*************************Pull out feedback****************************************8
	
	SELECT
	user_profile.first_name, batch_group.name, user_task_feedback.*
FROM
	batch_group,
	batch_students,
	user_task_feedback,
user_profile
WHERE
	batch_group.ID = batch_students.batch_group_id
and batch_students.student_id= user_task_feedback.user_id
and batch_group.id=21
and user_task_feedback.user_id=user_profile.user_id

****************************************************************************************



************************Track indivual student attandace details*******************************

Select user_id, COUNT (DISTINCT attendance. ID) FILTER (

WHERE
attendance.status = 'PRESENT'
) AS PRESENT_ABSENT from attendance where user_id in (7032,7050,7013
,7041
,7016
,7023
,7034
,7030)
GROUP BY user_id
***********************************************************************************


****************************************Trainer hours (elt)***********************************************

SELECT
	user_profile.user_id,
user_profile.first_name,
SUM(batch_schedule_event.eventhour)
FROM
	batch_schedule_event,
user_profile
WHERE
	eventdate > '2017-06-28'
AND eventdate < '2017-07-27'
AND TYPE = 'BATCH_SCHEDULE_EVENT_TRAINER'
AND batch_schedule_event.actor_id = user_profile.user_id
GROUP BY
user_profile.user_id,
user_profile.first_name

**associate_trainee

SELECT
	*
FROM
	batch_schedule_event
WHERE
	actor_id = '10533'
AND created_at > '2017-10-28'
AND associate_trainee = '7664'						

**single trainee


select * from batch_schedule_event where actor_id = 7664 and created_at > '2017-10-28'


*****************************************************************************************************




***************************************Trainer hours (api)***********************************************


SELECT
	student. NAME AS trainer_name,
	student.email AS trainer_email,
	SUM (
		batch_schedule_event.eventhour
	) AS trainer_hrs,
	SUM (
		batch_schedule_event.eventminute
	) AS trainer_min,
	college. NAME AS org_name
FROM
	batch_schedule_event,
	student,
	college,
	classroom_details
WHERE
	eventdate > '2017-05-28'
AND eventdate < '2017-06-27'
AND TYPE = 'BATCH_SCHEDULE_EVENT_TRAINER'
AND student. ID = batch_schedule_event.actor_id
AND batch_schedule_event.classroom_id = classroom_details. ID
AND classroom_details.organization_id = college. ID
GROUP BY
	student. NAME,
	college. NAME,
	student.email
	
	
*****************************************************************************************************




********************************student password****************************************
SELECT
first_name,
last_name,
mobile,
password,
email
FROM
user_profile,
istar_user
WHERE
istar_user. ID = user_profile.user_id
AND user_profile.user_id IN (
SELECT
student_id
FROM
batch_students
WHERE
batch_group_id = 29
)
add password to that 



*****************************Delete user***************************

delete from istar_user where id = 10345

delete from user_profile where user_id =10345

delete from user_role where user_id =10345 

delete from professional_profile where user_id = 10345

delete from batch_students where student_id = 10345

delete from user_org_mapping where user_id = 10345


***********************************************************************************


*****************************Add student into a batch_group**************************

INSERT INTO batch_students (
	ID,
	batch_group_id,
  student_id,
  user_type
)
VALUES
	(
		(
			SELECT
				MAX (ID) + 1
			FROM
				batch_students
		),
		149,
		4646,
		'STUDENT'
	);
	
	***************************************************************************



*************************warangal***********************************************
DVR
u.n= admin
pwd= admin


NVR
u.n=123456abc
pwd=admin

U.n= telecomadmin
pwd= admintelecom

Static iP  117.220.198.2
admin
123456abc
**********************************************************************************


***************************Ranchi*************************************************

Static ip 103.27.140.11


NVR and DVR
admin
admin12345

**********************************************************************************



***************************Patna**************************************************




	
	

	
	
