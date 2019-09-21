1. Managing Users
The user_account table has the following columns:

id – This is both the table’s primary key and a unique identifier for each user. This ID will be referred to by other tables in the data model.
user_type_id – This signifies whether the user is a job seeker or a employer.
email – This column holds the user’s email address.
password – This stores an encrypted account password (created by users during registration).
date_of_birth and gender – As their names suggest, these columns hold users’ date of birth and gender.
is_active – Initially this column would be “Y”, but users can set their profile to inactive, or “N”. This column stores their choice.
contact_number – This is the phone number (usually mobile) provided during registration. Users can receive SMS (text) notifications on this number. It can be the same number (or not) as the one job seekers list in their profile or resume.
sms_notification_active and email_notification_active
user_image – This is a BLOB-type attribute that stores each user’s profile image. 
registration_date – This column keeps a record of when the user registered.

2. Building Profiles
In the company table, we have the following columns:

id – The primary key of this table is also used to uniquely identify companies.
company_name – This holds the legal name of a company.
profile_description – This contains a brief description of each company.
business_stream_id – This column depicts which business stream a company belongs to.
establishment_date – This column tells you how old a company is.
company_website_url – This is a mandatory (non-nullable) column. 

Job Seeker Profiles

The seeker_profile table holds additional details that were not captured during the registration process. It contains these fields:

user_account_id – This column is referred from the user_account table, and it acts as the primary key for this table. It ensures there will be a maximum of one profile per job seeker.
first_name and last_name –Hold the job seeker’s first and last names.
current_salary – This attribute contains the job seeker’s current salary. It is nullable because people may not want to disclose it.
is_annually_monthly – This defines whether their salary amount is per year or per month.
currency – This stores the currency of the salary.
The education_detail table stores each job seeker’s educational history, as provided by them. It has a composite primary key made up of the user_account_id, certificate_degree_name and major columns. This ensures that users enter only one record for each degree or certificate. The table contains these attributes:

user_account_id – This column is referred from the user_account table and serves as the primary key for this table.
certificate_degree_name – This is the certificate or degree type.
major – This column holds the main course of study for the certificate or degree.
institute_university_name – This is the institute, school, or university that awarded the degree or certificate.
start_date – This attribute stores the date when the user was accepted into an educational program.
completion_date – This is the date the degree or certificate was awarded. However, this attribute is nullable; people may still be completing their program while they are looking for a job, or they may have dropped out of the program altogether.
percentage and cgpa – These columns store the grade percentage or CGPA (cumulative grade point average) attained by users in their degree or certificate course.

The experience_detail table keeps records of users’ past and current professional experience. It contains the following important columns:

user_account_id – This column is referred from the user_account table and is the primary key for this table.
is_current_job – This is an indicator column that signifies the user’s current job. This column also plays a major role in deriving users’ current locations and how long they’ve held their current position.
start_date – This stores when a user starts a job.
end_date – This stores when a user ends a job.
job_title – This holds information about the user’s job role.
company_name – This attributes holds the relevant company name associated with a job.
job_city – This signifies the city where the job was located.
job_state – This signifies the state where the job was located.
job_country – This signifies the country where the job was located.
description – This column stores details about job roles and responsibilities, challenges, and achievements.
Job seekers can possess multiple skills. To keep records of all of these skill sets, we’ll create the table seeker_skill_set. The columns are:

user_account_id – This column is referred from the user_account table and is the primary key for this table.
skill_set_id – This ID signifies which skill set the user possesses.
skill_level – This numeric attribute quantifies job seekers’ expertise in a particular skill. A number from 1 (beginner) to 10 (expert) indicates their experience level.

The skill_set table contains descriptions of all the skills referred to in the above table’s skill_set_id attribute. It contains only two columns, a skill_set_name and its related id.

3. Job Posting and Looking Up Jobs

job_post table Holds details about job posts. All the other tables in this section are created around it and linked with it.

id – This is the primary key of this table. Each job post is assigned a unique number, and this number is referred to in other tables.
posted_by_id – This column holds the register_user_id of the employer who has posted the job.
job_type_id – This column signifies whether the job duration is permanent or temporary (contract).
company_id – This column stores the ID of the company related to the job post. It is a reference to the company table.
is_company_name_hidden – This is a flag column that shows if the company’s name should be shown to job seekers. employers may prefer not to show company names on their post.
created_date – This stores the date when the job is posted.
job_description – This holds a brief description of the job.
job_location_id – This refers to an attribute in the job_location table that stores the actual location of the job: street address, city, state, country, and postal code.
is_active – This signifies if a job is still open. employers can mark their posts inactive as soon as the positions are filled.


The job_post_skill_set table stores details about the skill sets required for a job. The table structure is identical to the seeker_skill_set table.

The job_post_activity table, holds details about which job seekers apply for a job and when.