integer
string
decimal
temporal
special
custom


mysql> help int;


MariaDB sometimes silentyl truncates / rounds. Check sql_mode



AUTO_INCREMENT solo válido para INTEGER

LAST_INSERT_ID() return the latest auto_inc value generated by the curret client connection

SERIAL es a useful synonym for:
BIGINT UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE

InnoDB prepares auto_inc counters at mysqdl startup:
SELECT MAX(auto_inc_filed) FROM table
  Deleted rows could mean auto_inc values are resused - watch out!