# Windows için PostgreSQL Otomatik Yedek Alma(Backup) ve Yedek Kurma(Restore) 

@echo off
   for /f "tokens=1-4 delims=/ " %%i in ("%date%") do (
     set dow=%%i
     set month=%%j
     set day=%%k
     set year=%%l
   )
 
  for /f "tokens=1-3 delims=: " %%i in ("%time%") do (
	set hour=%%i
	set min=%%j
	set sec=%%k
     )		 
for /f "delims=" %%i in ('dir "%target_backup_path%" /b/a-d ^| find /v /c "::"') do set count=%%i
set /a count=%count%+1 
set datestr=%year%_%month%_%day%_%hour%_%min%  
   set BACKUP_FILE=yedek_%datestr%.backup
   SET PGPASSWORD=2018
   echo on
   pg_dump -h 15.15.15.15  -p 5432 -U postgres -F c -b -v -f %BACKUP_FILE% DB_Project
