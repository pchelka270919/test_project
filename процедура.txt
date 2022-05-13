CREATE OR REPLACE Procedure add_students_marks(last_name_in IN varchar2, lesson_name_in IN varchar2, question IN varchar2, is_activity IN boolean)
 IS
   student_id number;
   lesson_id number;
   activity_marker varchar(20) := null;
 
   cursor c1 is
   SELECT student_id
    FROM students
    WHERE last_name = last_name_in;
 
   cursor c2 is
   SELECT lesson_id
    FROM lessons
    WHERE lesson_name = lesson_name_in;
    
BEGIN
 
   if is_activity = true then
    activity_marker := '(+)';
   end if; 
   open c1;
   open c2;
   fetch c1 into student_id;
   fetch c2 into lesson_id;
  
   INSERT INTO students_lessons
   ( student_id,
     lesson_id,
     stud_mark,
     question,
     active_work)
   VALUES
   ( student_id,
     lesson_id,
     '+',
     question,
     activity_marker);
     
   commit;
 
   close c1;
   close c2;
 
EXCEPTION
WHEN OTHERS THEN
   raise_application_error(-20001,'An error was encountered - '||SQLCODE||' -ERROR- '||SQLERRM);
END;


CREATE OR REPLACE Procedure add_students_marks(last_name_in IN varchar2, lesson_name_in IN varchar2, question IN varchar2, is_activity IN varchar2)
 IS
   student_id number;
   lesson_id number;
 
   cursor c1 is
   SELECT student_id
    FROM students
    WHERE last_name = last_name_in;
 
   cursor c2 is
   SELECT lesson_id
    FROM lessons
    WHERE lesson_name = lesson_name_in;
    
BEGIN
 
   if is_activity := '(+)' then
    activity_marker := '(+)';
   else is_activity := NULL
   end if; 
   open c1;
   open c2;
   fetch c1 into student_id;
   fetch c2 into lesson_id;
  
   INSERT INTO students_lessons
   ( student_id,
     lesson_id,
     stud_mark,
     question,
     active_work)
   VALUES
   ( student_id,
     lesson_id,
     '+',
     question,
     activity_marker);
     
   commit;
 
   close c1;
   close c2;
 
EXCEPTION
WHEN OTHERS THEN
   raise_application_error(-20001,'An error was encountered - '||SQLCODE||' -ERROR- '||SQLERRM);
END;