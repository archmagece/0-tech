# postgresql


psql -U postgres

CREATE USER <username> WITH ENCRYPTED PASSWORD '<password>';
CREATE DATABASE <dbname>;
GRANT ALL PRIVILEGES ON DATABASE <dbname> TO <username>;
ALTER USER role_specification WITH OPTION1 OPTION2 OPTION3;
ALTER USER <username> WITH SUPERUSER;
ALTER USER <username> WITH NOSUPERUSER;

show database list
\list, \l

show database list with detail info
\list+, \l+

\du, \du+

show user
SELECT username FROM pg_user;


CREATE DATABASE confluence;

create user atlassian_user with encrypted password 'passwrod0000000';

grant all privileges on database confluence to atlassian_user;


CREATE DATABASE jira;

grant all privileges on database jira to atlassian_user;

