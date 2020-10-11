# PL/SQL

Client: Epsilon<br>
Duration: 4 full days<br>
From: 5th October 2020<br>
Mode: Online/ Microsoft Teams<br>

<h1><a href="https://courses.vinod.co/">Learn with Vinod</a></h1>

<pre>
 _      _____   ___  ______  _   _      _    _  _____  _____  _   _      _   _  _____  _   _  _____ ______ 
| |    |  ___| / _ \ | ___ \| \ | |    | |  | ||_   _||_   _|| | | |    | | | ||_   _|| \ | ||  _  ||  _  \
| |    | |__  / /_\ \| |_/ /|  \| |    | |  | |  | |    | |  | |_| |    | | | |  | |  |  \| || | | || | | |
| |    |  __| |  _  ||    / | . ` |    | |/\| |  | |    | |  |  _  |    | | | |  | |  | . ` || | | || | | |
| |____| |___ | | | || |\ \ | |\  |    \  /\  / _| |_   | |  | | | |    \ \_/ / _| |_ | |\  |\ \_/ /| |/ / 
\_____/\____/ \_| |_/\_| \_|\_| \_/     \/  \/  \___/   \_/  \_| |_/     \___/  \___/ \_| \_/ \___/ |___/  
                                                                                                           
                                                                                   
Vinod Kumar Kayartaya
Software trainer, independent consultant and freelance developer.
https://vinod.co
vinod@vinod.co
+91 973 142 4784
</pre>

<a href="https://www.youtube.com/channel/UCv5p6Zh6Sh6Pd7BQjgcNWog?sub_confirmation=1">
Please subscribe to my YouTube channel</a>

---

### Class notes:

### Day 1

<pre>
SELECT
    COUNT(*)
FROM
    employees;

SET SERVEROUTPUT ON

CL SCR

BEGIN
    dbms_output.put_line('Hello, world!');
END;
/

SELECT * FROM V$VERSION;

CL SCR
DECLARE
    V_EMPLOYEE_ID EMPLOYEES.EMPLOYEE_ID%TYPE := 102;
    V_SALARY EMPLOYEES.SALARY%TYPE;
BEGIN
    -- SELECT STATEMENTS ARE NOT REALLY SQL COMMANDS HERE.
    -- THEY ARE MODIFIED VERSION OF SQL
    SELECT SALARY INTO V_SALARY
    FROM EMPLOYEES
    WHERE EMPLOYEE_ID = V_EMPLOYEE_ID;
        
    DBMS_OUTPUT.PUT_LINE('SALARY OF EMPLOYEE WITH ID ' || V_EMPLOYEE_ID || ' IS $' || V_SALARY);
END;
/

cl scr
DECLARE
    x   NUMBER(10);
    y   NUMBER(10);
    z   NUMBER(10);
BEGIN
    x := 100;
    y := 200;
    z := x + y;
    
    dbms_output.put_line('Z IS ' || z);
END;
/
print z;



CL SCR
DECLARE
    V_EMP EMPLOYEES%ROWTYPE;
BEGIN
    V_EMP.EMPLOYEE_ID := 102;
    
    -- SELECT STATEMENTS ARE NOT REALLY SQL COMMANDS HERE.
    -- THEY ARE MODIFIED VERSION OF SQL
    SELECT * INTO V_EMP
    FROM EMPLOYEES
    WHERE EMPLOYEE_ID = V_EMP.EMPLOYEE_ID;
        
    DBMS_OUTPUT.PUT_LINE('FIRSTNAME = ' || V_EMP.FIRST_NAME);
    DBMS_OUTPUT.PUT_LINE('LASTNAME  = ' || V_EMP.LAST_NAME);
    DBMS_OUTPUT.PUT_LINE('SALARY    = $' || V_EMP.SALARY);
END;
/

CL SCR
-- THIS VARIABLE IS PART OF THE TOOL (SQL DEVELOPER) OR PART OF THE CLIENT APP (EX:JAVA)
VARIABLE B_SALARY NUMBER;
PRINT B_SALARY;

BEGIN
    SELECT SALARY INTO :B_SALARY
    FROM EMPLOYEES
    WHERE EMPLOYEE_ID = 103;
END;
/
PRINT B_SALARY;


CL SCR
DECLARE
    NAME VARCHAR(20):= 'VINOD KUMAR';
    LEN NUMBER;
    MAX_SAL NUMBER;
BEGIN
    LEN := LENGTH(NAME);
    -- SELECT LENGTH(NAME) INTO LEN FROM DUAL;
    DBMS_OUTPUT.PUT_LINE('LEN IS ' || LEN);
    
    SELECT MAX(SALARY) INTO MAX_SAL
    FROM EMPLOYEES;
    DBMS_OUTPUT.PUT_LINE('MAX_SAL IS ' || MAX_SAL);
END;
/

DESC DUAL;
SELECT * FROM DUAL;
SELECT LENGTH('VINOD KUMAR KAYARTAYA') FROM DUAL;


CL SCR

<<BLK1>>DECLARE
    name   VARCHAR(50) := 'HARISH';
    age    NUMBER := 40;
BEGIN
    dbms_output.put_line(name
                         || ' IS '
                         || age
                         || ' YEARS OLD');
    <<BLK2>>DECLARE
        name   VARCHAR(50) := 'MAHESH';
        age    NUMBER := 50;
    BEGIN
        dbms_output.put_line(NAME || ' AND ' || BLK1.NAME || ' ARE FRIENDS.');
        dbms_output.put_line(name
                             || ' IS '
                             || age
                             || ' YEARS OLD');
    END;

END;
/




CL SCR
DECLARE
    V_EMP EMPLOYEES%ROWTYPE;
BEGIN
    V_EMP.EMPLOYEE_ID := &EMPLOYEE_ID;
    
    -- SELECT STATEMENTS ARE NOT REALLY SQL COMMANDS HERE.
    -- THEY ARE MODIFIED VERSION OF SQL
    SELECT * INTO V_EMP
    FROM EMPLOYEES
    WHERE EMPLOYEE_ID = V_EMP.EMPLOYEE_ID;
        
    DBMS_OUTPUT.PUT_LINE('FIRSTNAME = ' || V_EMP.FIRST_NAME);
    DBMS_OUTPUT.PUT_LINE('LASTNAME  = ' || V_EMP.LAST_NAME);
    DBMS_OUTPUT.PUT_LINE('SALARY    = $' || V_EMP.SALARY);
END;
/


SELECT FIRST_NAME, LAST_NAME, SALARY 
FROM EMPLOYEES WHERE DEPARTMENT_ID = 20;

CL SCR
-- THIS CODE WORKS ONLY FOR DEPARTMENTS WITH EXACT 1 EMPLOYEE ROW IN THE GIVEN DEPARTMENT
DECLARE
    V_FIRST_NAME VARCHAR(20);
    V_LAST_NAME VARCHAR(20);
    V_SALARY NUMBER(8,2);
BEGIN
    SELECT FIRST_NAME, LAST_NAME, SALARY
    INTO V_FIRST_NAME, V_LAST_NAME, V_SALARY
    FROM EMPLOYEES WHERE DEPARTMENT_ID = 10;
    
    DBMS_OUTPUT.PUT_LINE('FIRSTNAME = ' || V_FIRST_NAME);
    DBMS_OUTPUT.PUT_LINE('LASTNAME  = ' || V_LAST_NAME);
    DBMS_OUTPUT.PUT_LINE('SALARY    = $' || V_SALARY);
END;
/

CL SCR
DECLARE
    V_AVG_SAL NUMBER;
    V_MAX_SAL NUMBER;
    V_MIN_SAL NUMBER;
BEGIN
    SELECT AVG(SALARY), MAX(SALARY), MIN(SALARY)
        INTO V_AVG_SAL, V_MAX_SAL, V_MIN_SAL
        FROM EMPLOYEES;

    DBMS_OUTPUT.PUT_LINE('AVG SALARY = $' || V_AVG_SAL);
    DBMS_OUTPUT.PUT_LINE('MAX SALARY = $' || V_MAX_SAL);
    DBMS_OUTPUT.PUT_LINE('MIN SALARY = $' || V_MIN_SAL);
END;



-- EXAMPLE OF USING IMPLICIT CURSOR ATTRIBUTES
CL SCR
DECLARE
    V_DEPARTMENT_ID NUMBER := &DEPARTMENT_ID;
BEGIN
    UPDATE EMPLOYEES
    SET SALARY = SALARY * 1.1
    WHERE DEPARTMENT_ID = V_DEPARTMENT_ID;
    
    DBMS_OUTPUT.PUT_LINE('SALARY OF ' || SQL%ROWCOUNT || ' EMPLOYEES HIKED');
    COMMIT;
END;

-- EXAMPLE USAGE OF IF STATEMENTS
CL SCR

DECLARE
    v_first_name   employees.first_name%TYPE;
    v_salary       employees.salary%TYPE;
    v_msg          VARCHAR(100);
BEGIN
    SELECT
        first_name,
        salary
    INTO
        v_first_name,
        v_salary
    FROM
        employees
    WHERE
        employee_id = 174;

    IF v_salary >= 15000 THEN
        v_msg := v_first_name || ' IS A CATEGORY-A EMPLOYEE';
    ELSIF v_salary >= 10000 THEN
        v_msg := v_first_name || ' IS A CATEGORY-B EMPLOYEE';
    ELSE
        v_msg := v_first_name || ' IS A CATEGORY-C EMPLOYEE';
    END IF;

    dbms_output.put_line(v_msg);
END;
/

-- EXAMPLE OF A CASE STATEMENT

CL SCR

DECLARE
    v_first_name   employees.first_name%TYPE;
    v_salary       employees.salary%TYPE;
    v_msg          VARCHAR(100);
BEGIN
    SELECT
        first_name,
        salary
    INTO
        v_first_name,
        v_salary
    FROM
        employees
    WHERE
        employee_id = 104;
        
    v_msg := v_first_name || ' IS A CATEGORY-' || case 
        WHEN v_salary >= 15000 THEN 'A'
        WHEN v_salary >= 10000 THEN 'B'
        ELSE 'C'
    end || ' EMPLOYEE';
    
    dbms_output.put_line(v_msg);
END;
/


cl scr
declare
    v_grade char := upper('&grade');
    v_appraisal varchar(100);
begin
    v_appraisal := case v_grade
        when 'A' then 'Excellent'
        when 'B' then 'Very good'
        when 'C' then 'Good'
        else 'You have input an invalid value for grade; must be one of A or B or C'
    end;
    
    dbms_output.put_line(v_appraisal);
end;
/

declare
    v_count number(10) := 1;
begin
    loop
        dbms_output.put_line('This is loop number ' || v_count);
        v_count := v_count + 1;
        exit when v_count > 10;        
    end loop;
end;
/

declare
    v_count number(10) := 1;
begin
    while v_count <= 10
    loop
        dbms_output.put_line('This is loop number ' || v_count);
        v_count := v_count + 1;
    end loop;
end;
/

declare
    v_num number(10);
    v_sqr number(10);
begin
    loop
        -- SQL developer tool sends the actual PL/SQL block to the remote server only
        -- after substituing the value for &NUMBER. This means, server runs the loop
        -- indefinitely.
        v_num := &NUMBER;
        
        exit when v_num = 0;
        
        v_sqr := v_num * v_num;
        dbms_output.put_line(v_sqr);
    end loop;
end;
/


declare
    nu number(3) := &NUMBER;
    li number(2) := 10;
    pr number(3);
begin

    for i in 1..10
    loop
        pr := nu * i;
        dbms_output.put_line(nu || ' X ' || i || ' = ' || pr);
    end loop;
end;
/

DECLARE
    i     NUMBER := 1;
    j     NUMBER;
    str   VARCHAR(50) := '';
BEGIN
    << loop1 >> LOOP
        j := 1;
        << loop2 >> LOOP
            str := str || '* ';
            j := j + 1;
            EXIT loop1 WHEN i > 10;
            EXIT WHEN j > i;
        END LOOP;

        dbms_output.put_line(str);
        str := '';
        i := i + 1;
        
    END LOOP;
END;
/


BEGIN
    
    for i in 1..20
    loop
    
        if i mod 3 = 0 then 
            continue;
        end if;
    
        dbms_output.put_line(i);
    end loop;
    
END;
/

declare
    type empl is record (
        fname varchar(20),
        lname varchar(20),
        sal number(8,2)
    );
    
    e1 empl;
begin
    select first_name, last_name, salary
    into e1
    from employees 
    where employee_id = 107;
    
    dbms_output.put_line('Name   = ' || e1.fname || ' ' || e1.lname);
    dbms_output.put_line('Salary = $' || e1.sal);
end;
/


declare
    type empl is record (
        fname employees.first_name%type,
        lname employees.last_name%type,
        sal employees.salary%type
    );
    
    e1 empl;
begin
    select first_name, last_name, salary
    into e1
    from employees 
    where employee_id = 101;
    
    dbms_output.put_line('Name   = ' || e1.fname || ' ' || e1.lname);
    dbms_output.put_line('Salary = $' || e1.sal);
end;
/

declare
    e1 employees%rowtype;
begin
    select * into e1
        from employees
        where employee_id = 109;
        
    dbms_output.put_line('Name   = ' || e1.first_name || ' ' || e1.last_name);
    dbms_output.put_line('Salary = $' || e1.salary);
    dbms_output.put_line('DOJ    = ' || to_char(e1.hire_date, 'Month DD, YYYY'));
end;
/

declare
    j jobs%rowtype;
begin
    j.job_id := 'XYZ';
    j.job_title := 'Test Job Title';
    j.min_salary := 5000;
    j.max_salary := 15000;
    
    insert into jobs values j;
    commit;
end;
/


declare
    e1 employees%rowtype;
begin
    select * into e1 from employees where employee_id = 109;
    
    -- modify values in e1, based on values received from the client app (TBD)
    e1.salary := 12000;
    e1.email := 'DANIET';
    e1.manager_id := 107;
    
    -- update values in e1 to the db table
    update employees 
        set row = e1 
        where employee_id = e1.employee_id;
        
    commit;
end;
/



DECLARE
    TYPE friends_type IS
        TABLE OF VARCHAR(255) INDEX BY BINARY_INTEGER;
    
    fr friends_type;
    id binary_integer;
BEGIN 

    fr(100) := 'VINOD';
    fr(200) := 'SHYAM';
    fr(239) := 'RAMESH';
    fr(345) := 'VISHAL';
    
    id := fr.FIRST;
    while id is not null
    loop
        dbms_output.put_line('id = ' || id || ', name = ' || fr(id));
        id := fr.NEXT(id);
    end loop;
end;
/
</pre>

### Day 2

<pre>
CL SCR; 

SELECT
     first_name || ' ' || last_name || q'['s monthly salary is $]' || salary as Description,
     salary *.22 q_bonus,
     commission_pct
 FROM
     employees
 WHERE
     commission_pct is not NULL;
     
     
select distinct job_id from employees;

desc employees;

select first_name, last_name, hire_date from employees order by hire_date;


cl scr
SELECT
    first_name,
    last_name,
    hire_date
FROM
    employees
WHERE
    hire_date < '01-jan-2004'
ORDER BY
    hire_date;
    
-- ---------------------------------------------------
CL SCR

SELECT
    *
FROM
    employees
WHERE
    hire_date BETWEEN '01-jan-2004' AND '31-dec-2004';

-- ---------------------------------------------------
CL SCR

SELECT
    *
FROM
    employees
WHERE
    hire_date not BETWEEN '01-jan-2004' AND '31-dec-2004';

-- ---------------------------------------------------
CL SCR

SELECT * FROM EMPLOYEES
WHERE SALARY NOT BETWEEN 16000 AND 17000;


-- ---------------------------------------------------
CL SCR

SELECT * FROM EMPLOYEES
WHERE DEPARTMENT_ID IS NULL


-- ---------------------------------------------------
CL SCR


SELECT * FROM EMPLOYEES
WHERE FIRST_NAME LIKE 'K%';


SELECT * FROM EMPLOYEES
WHERE FIRST_NAME LIKE 'K%n';


SELECT * FROM EMPLOYEES
WHERE FIRST_NAME LIKE '___a%';

SELECT * FROM EMPLOYEES
WHERE HIRE_DATE LIKE '__-01-04'

select * from employees 
where not salary > 15000


SELECT FIRST_NAME, LAST_NAME, SALARY, JOB_ID
FROM EMPLOYEES
WHERE (JOB_ID = 'SA_REP' OR JOB_ID='AD_PRES') AND SALARY>=10000;


SELECT FIRST_NAME, LAST_NAME, SALARY, JOB_ID, HIRE_DATE FROM EMPLOYEES 
ORDER BY JOB_ID, SALARY DESC, LAST_NAME;


-- EXAMPLE OF SINGLE-ROW-FUNCTION WITH COLUMN/EXPRESSION
SELECT FIRST_NAME, UPPER(FIRST_NAME || ' ' || LAST_NAME) FULLNAME,
LENGTH(UPPER(FIRST_NAME || ' ' || LAST_NAME))
FROM EMPLOYEES;

-- MULTIROW (AGGREGATE/GROUP) FUNCTION
SELECT COUNT(FIRST_NAME) FROM EMPLOYEES;

-- LENGTH WITH STRING LITERAL
SELECT LENGTH('VINOD KUMAR KAYARTAYA') FROM DUAL;

SELECT UPPER('VINOD KUMAR kayartaya'), 
    lower('VINOD KUMAR KAYARTAYA'),
    initcap('VINOD KUMAR KAYARTAYA'),
    substr('VINOD KUMAR KAYARTAYA', 7, 5) from dual;
    
select '*' || ltrim('            vinod      kumar     ') || '*',
    '*' || rtrim('            vinod       kumar    ') || '*',
    '*' || trim('            vinod        kumar   ') || '*'
    from dual;
    
    

select lpad('vinod kumar', 25, '~'), 
    rpad('vinod', 25, '~'), concat('vinod', 'kumar') from dual;
    
select mod(12345, 123) from dual;


select first_name, last_name, hire_date, to_char(hire_date, 'DD-MON-YYYY') DOJ from employees;

SELECT
    sysdate,
    sysdate + 10,
    round((sysdate - TO_DATE('20-jan-1974', 'DD-MON-YYYY')) / 365, 2) age
FROM
    dual;


-- begining and NEXT year
select trunc(SYSDATE, 'YEAR'), round(sysdate, 'YEAR') from dual;
SELECT
    first_name
    || ' JOINED THE COMPANY ON '
    || hire_date
    || ' AND EARNS A SALARY OF $'
    || salary
    || ' PER MONTH' AS description
FROM
    employees;


SELECT HIRE_DATE, TO_CHAR(HIRE_DATE, 'YEAR') YEAR FROM EMPLOYEES WHERE EMPLOYEE_ID = 100;


SELECT TO_CHAR(SYSDATE+20, 'fmDAY MONTH dd, YYYY') FROM DUAL;


SELECT
    to_char(5678.87354321, '999,999,999.99'),
    to_char(5678.87354321, '000,000,000.00'),
    to_char(23456, '999,999,990.00'),
    to_char(23456, '$999,999,990.00'),
    to_char(23456, 'L999,999,990.00')
FROM
    dual;

SELECT
    first_name,
    last_name,
    salary,
    commission_pct,
    ( salary + salary * nvl(commission_pct,.1) ) * 2 AS bonus
FROM
    employees;

SELECT
    first_name,
    last_name,
    salary,
    commission_pct,
    salary + nvl2(commission_pct, salary * commission_pct, salary *.15) AS bonus
FROM
    employees;


SELECT
    first_name,
    last_name,
    salary,
    NVL(TO_CHAR(commission_pct), 'NO COMMISSION') COMM_PCT,
    NVL(TO_CHAR(manager_id), 'NO MANAGER') MGR_ID,
    coalesce(TO_CHAR(commission_pct), TO_CHAR(manager_id), 'NO COMMISSION/MANAGER') result
FROM
    employees;


SELECT
    first_name,
    last_name,
    salary,
    CASE
        WHEN salary >= 15000 THEN
            'GRADE-A'
        WHEN salary >= 10000 THEN
            'GRADE-B'
        ELSE
            'GRADE-C'
    END AS grade
FROM
    employees
ORDER BY
    salary;



SELECT
    first_name,
    last_name,
    job_id,
    decode(job_id, 
        'AC_MGR', 'Accounting Manager', 
        'FI_MGR', 'Finance Manager',
        'SA_REP', 'Sales Representative', 
        'UNKNOWN') job_title
FROM
    employees;

-- ***** -- ***** -- ***** -- ***** -- ***** -- ***** -- ***** -- ***** 

SELECT
    first_name,
    last_name,
    job_id,
    CASE
        WHEN JOB_ID LIKE '%MGR' THEN 'MANAGER'
        WHEN JOB_ID LIKE '%ASST' THEN 'ASSISTENT'
        WHEN JOB_ID LIKE '%PROG' THEN 'PROGRAMMER'
        ELSE 'UNKNOWN'
    END job_title
FROM
    employees;

SELECT COUNT(*), -- COUNT OF ROWS (* INDICATES ALL COLUMNS OF ONE ROW)
    COUNT(SALARY),
    MAX(SALARY),
    MIN(SALARY),
    AVG(SALARY),
    SUM(SALARY),
    MIN(FIRST_NAME), MAX(FIRST_NAME)
    FROM EMPLOYEES;


SELECT COUNT(*), COUNT(FIRST_NAME), COUNT(COMMISSION_PCT) FROM EMPLOYEES;

SELECT COUNT(JOB_ID), COUNT(DISTINCT JOB_ID) FROM EMPLOYEES;

SELECT DISTINCT JOB_ID FROM EMPLOYEES;

SELECT AVG(COMMISSION_PCT), SUM(COMMISSION_PCT), COUNT(COMMISSION_PCT), 
    SUM(COMMISSION_PCT) / COUNT(COMMISSION_PCT) AS AVG_COMM_PCT,
    AVG(NVL(COMMISSION_PCT, 0)),
    SUM(COMMISSION_PCT) / COUNT(*) AS AVG_COMM_PCT_2
    FROM EMPLOYEES;
    
SELECT
    department_id,
    COUNT(*) no_of_emps,
    round(AVG(salary), 0) avg_salary,
    MAX(salary) max_salary
FROM
    employees
GROUP BY
    department_id
    
-- ++ -- -- ++ -- -- ++ -- -- ++ -- -- ++ -- -- ++ -- -- ++ -- -- ++ -- -- ++ -- 
SELECT
    department_id,
    job_id,
    COUNT(*) no_of_emps,
    round(AVG(salary), 0) avg_salary,
    MAX(salary) max_salary
FROM
    employees
GROUP BY
    department_id,
    job_id
ORDER BY
    DEPARTMENT_ID, JOB_ID;
    


--  "group function is not allowed here" (IN THE WHERE CLAUSE)
SELECT FIRST_NAME, LAST_NAME, SALARY
FROM EMPLOYEES
WHERE AVG(SALARY) <= 4000;

SELECT JOB_ID, AVG(SALARY)
FROM EMPLOYEES
GROUP BY JOB_ID
HAVING AVG(SALARY)>=10000


SELECT DEPARTMENT_ID, COUNT(*) NO_OF_EMPS -- THIS ALIAS IS CREATED ONLY AFTER THE EXECUTION OF HAVING CLAUSE
FROM EMPLOYEES
GROUP BY DEPARTMENT_ID
HAVING COUNT(*)<10 -- AT THIS TIME, THE ALIAS NO_OF_EMPS IS NOT CREATED; HENCE CANNOT BE USED
ORDER BY NO_OF_EMPS;

SELECT JOB_ID, COUNT(*), MAX(SALARY), AVG(SALARY) AVG_SAL FROM EMPLOYEES
WHERE JOB_ID NOT LIKE '%REP%'
GROUP BY JOB_ID
HAVING COUNT(*)>1
ORDER BY AVG_SAL


SELECT MAX(AVG(SALARY))
FROM EMPLOYEES
GROUP BY DEPARTMENT_ID;

SELECT
    first_name,
    last_name,
    department_name,
    location_id,
    e.department_id
FROM
    employees e,
    departments
WHERE
    E.department_id = departments.department_id
    
</pre>

### Day 3

<pre>
SELECT
    department_id
FROM
    departments;

SELECT
    *
FROM
    employees
WHERE
    employee_id = 100;

-- following won't work; since 900 is not one of existing department_id values in departments table

UPDATE employees
SET
    department_id = 900
WHERE
    employee_id = 100;
    
    
SELECT 
    employee_id,
    first_name
    || ' '
    || last_name employee_name,
    department_name
FROM
    employees,
    departments
WHERE employees.department_id = departments.department_id
    order by employee_id;
    
    
    
select departments.department_id, department_name, count(*) emp_count
    from employees, departments
    WHERE employees.department_id = departments.department_id
    group by departments.department_id, department_name
    order by departments.department_id;


    
-- join/using
SELECT
    employee_id,
    first_name
    || ' '
    || last_name employee_name,
    department_name
FROM
    employees
    JOIN departments
    using (department_id);
    
    
SELECT 
    employee_id,
    first_name
    || ' '
    || last_name employee_name,
    department_name
FROM
    employees
    JOIN departments using (department_id)

SELECT
    e.last_name,
    d.department_name,
    d.location_id,
    l.city
FROM
    employees     e
    JOIN departments   d ON e.department_id = d.department_id
    JOIN locations     l ON d.location_id = l.location_id
WHERE
    e.commission_pct IS NOT NULL;
    
    
    
-- using the natural join
SELECT
    department_name,
    city,
    state_province
FROM
    departments
    NATURAL JOIN locations;
    
SELECT
    first_name,
    last_name,
    salary,
    department_name,
    city,
    state_province
FROM
    employees
    JOIN departments ON employees.department_id = departments.department_id
    JOIN locations ON locations.location_id = departments.location_id;


SELECT
    first_name,
    last_name,
    salary,
    department_name
FROM
    employees
    JOIN departments USING ( department_id )
    JOIN locations USING ( location_id )
WHERE
    city = 'Oxford';



SELECT
    employees.first_name
    || ' '
    || employees.last_name employee_name,
    employees.salary employee_salary,
    managers.first_name
    || ' '
    || managers.last_name manager_name,
    managers.salary manager_salary
FROM
    employees
    join employees managers on employees.manager_id = managers.employee_id;


-- LIST OF ALL EMPLOYEES WHO HAVE THE SAME DEPARTMENT_ID AS 'NEENA'
SELECT
    employees.*
FROM
    employees 
    JOIN employees neena ON employees.department_id = neena.department_id
WHERE
    neena.first_name = 'Neena'
    
    
    
-- LIST OF ALL EMPLOYEES WHO EARN MORE THAN 'CLARA'
-- SELECT * FROM EMPLOYEES WHERE SALARY > 10500;
SELECT
    employees.*
FROM
    employees
    JOIN employees clara ON employees.salary > clara.salary
WHERE
    clara.first_name = 'Clara';

SELECT
    e1.*
FROM
    employees   e1
    JOIN employees   e2 ON e1.salary > e2.salary
WHERE
    e2.first_name = 'Clara';
    
    
-- list of all employees who report to the same manager (148) as Lisa Ozer with email 'LOZER'
-- select * from employees where manager_id = 148;
SELECT
    e1.*
FROM
    employees   e1
    JOIN employees   e2 -- LOZER'S record
     ON e1.manager_id = e2.manager_id
WHERE
    e2.email = 'LOZER'; 
    
    
-- list of all employees who have joined the company before Lisa Ozer (LOZER)
SELECT
    e1.*
FROM
    employees   e1
    JOIN employees   e2 ON e1.hire_date < e2.hire_date
WHERE
    e2.email = 'LOZER';
    
  
SELECT
    first_name || ' ' || last_name employee_name,
    department_name
FROM
    employees     e
    left JOIN departments   d ON e.department_id = d.department_id;


SELECT
    first_name
    || ' '
    || last_name employee_name,
    department_name
FROM
    employees e, departments   d
WHERE
    e.department_id (+)= d.department_id;

SELECT
    *
FROM
    employees
WHERE
    salary > (
        SELECT
            salary
        FROM
            employees
        WHERE
            last_name = 'Abel'
    )



SELECT
    *
FROM
    employees
WHERE
    salary > (
        SELECT
            AVG(salary)
        FROM
            employees
    )

SELECT
    *
FROM
    employees
WHERE
    salary = (
        SELECT
            MIN(salary)
        FROM
            employees
    );


SELECT
    department_id,
    MIN(salary) min_dept_sal
FROM
    employees
GROUP BY
    department_id
HAVING
    MIN(salary) > (
--MINIMUM SALARY IN DEPARTMENT 80
        SELECT
            MIN(salary)
        FROM
            employees
        WHERE
            department_id = 80
    )
ORDER BY
    min_dept_sal


SELECT * FROM EMPLOYEES
WHERE SALARY = (
SELECT MIN(SALARY) FROM EMPLOYEES GROUP BY DEPARTMENT_ID
)


SELECT * FROM EMPLOYEES
WHERE JOB_ID = (
SELECT JOB_ID FROM EMPLOYEES WHERE FIRST_NAME = 'VINOD'
)


-- JOB_ID OF ALL EMPLOYEES WHO ARE REPORTING TO 'Nancy'
SELECT JOB_ID FROM EMPLOYEES WHERE MANAGER_ID  = (
    SELECT EMPLOYEE_ID FROM EMPLOYEES WHERE FIRST_NAME = 'Nancy'
)

-- LIST OF EMPLOYEES WHO HAVE THE SAME JOB_ID AS ANY  EMPLOYEES WORKING UNDER THE MANAGER 'Nancy'
SELECT * FROM EMPLOYEES WHERE JOB_ID IN (
    SELECT JOB_ID FROM EMPLOYEES WHERE MANAGER_ID  = (
        SELECT EMPLOYEE_ID FROM EMPLOYEES WHERE FIRST_NAME = 'Nancy'
    )
)

-- LOCATION INFORMATION OF ALL EMPLOYEES WITH JOB_IDs AS ANY EMPLOYEE REPORTING TO 'Nancy'
SELECT DISTINCT E.JOB_ID, L.* 
FROM EMPLOYEES E
JOIN DEPARTMENTS D ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
JOIN LOCATIONS L ON D.LOCATION_ID = L.LOCATION_ID
WHERE JOB_ID IN (
    SELECT JOB_ID FROM EMPLOYEES WHERE MANAGER_ID  = (
        SELECT EMPLOYEE_ID FROM EMPLOYEES WHERE FIRST_NAME = 'Neena'
    )
)


-- < any (list of values) ---> less than largest in the list
-- > any (list of values) ---> greater than the smallest in the list

-- < all (list of values) ---> less than smallest in the list
-- > all (list of values) ---> greater than the largest in the list
SELECT
    first_name,
    salary
FROM
    employees
WHERE
    salary < ALL (
        SELECT
            salary
        FROM
            employees
        WHERE
            job_id = 'IT_PROG'
    )
    AND job_id != 'IT_PROG'


SELECT
    department_id,
    employee_id,
    first_name,
    last_name,
    salary
FROM
    employees e1
WHERE
    salary = (
    -- maximum salary in e1's department
    select max(salary) from employees where department_id = e1.department_id
)
ORDER BY
    department_id,
    salary DESC


-- ex-1
-- Write a query to display the lastname, department number, and department name for all employees.
SELECT
    last_name,
    department_id,
    department_name
FROM
    employees
    JOIN departments USING ( department_id );



-- ex-2
-- Create a unique listing of all jobs that are in department 30. Include the location id in the output.

SELECT DISTINCT
    job_title,
    location_id
FROM
    employees
    JOIN departments USING ( department_id )
    JOIN jobs USING ( job_id )


-- ex-3
-- Write a query to display the employee lastname, department name, location id, and city of all employees who earn a commission.

SELECT
    e1.last_name,
    d1.department_name,
    d1.location_id,
    l1.city
FROM
    employees     e1
    JOIN departments   d1 ON e1.department_id = d1.department_id
    JOIN locations     l1 ON d1.location_id = l1.location_id
WHERE
    e1.commission_pct IS NOT NULL;
    
    
    
-- ex-4
-- Display the employee lastname, and department name for all employees who have an “a” in their lastname.

SELECT
    last_name,
    department_name
FROM
    employees
    JOIN departments USING ( department_id )
WHERE
    lower(last_name) LIKE '%a%';
    
 
-- ex-5
-- Write a query to display the lastname, job, department number, and department name for all employees who work in Toronto.

SELECT
    e1.last_name,
    j1.job_title,
    d1.department_id,
    d1.department_name
FROM
    employees     e1
    JOIN jobs          j1 ON e1.job_id = j1.job_id
    JOIN departments   d1 ON e1.department_id = d1.department_id
    JOIN locations     l1 ON d1.location_id = l1.location_id
WHERE
    l1.city = 'Toronto'

-- ex-6
-- Display the employee lastname and employee number along with their manager’s lastname and manager number. 
-- Label the columns “Employee”, “Emp#”, “Manager” and “Manager#” respectively.

SELECT
    emp.last_name  "Employee",
    emp.employee_id   "Emp#",
    mgr.last_name     "Manager",
    mgr.employee_id   "Manager#"
FROM
    employees   emp
    JOIN employees   mgr ON emp.manager_id = mgr.employee_id

-- ex-7
-- Modify the above to display the same columns for all employees (including “King”, who has no manager). 
-- Order the result by the employee number.

SELECT
    emp.last_name  "Employee",
    emp.employee_id   "Emp#",
    mgr.last_name     "Manager",
    mgr.employee_id   "Manager#"
FROM
    employees   emp
    left JOIN employees   mgr ON emp.manager_id = mgr.employee_id
order by "Emp#"

-- ex-8
-- Create query that displays employee lastnames, department numbers of all the employees 
-- who work in the same department as a given employee. Give each column an appropriate label.

-- using self join::
SELECT
    e1.last_name,
    e1.department_id
FROM
    employees   e1
    JOIN employees   e2 ON e1.department_id = e2.department_id
                         AND e2.employee_id = 101

-- using subquery::
SELECT
    last_name,
    department_id
FROM
    employees
WHERE
    department_id = (
        SELECT
            department_id
        FROM
            employees
        WHERE
            employee_id = 101
    );

    
-- ex-9
-- Create a query that displays the name, job, department name, salary and grade for all employees.
-- SAL_GRADE TABLE IS MISSING

/*
CREATE TABLE SAL_GRADES(
    GRADE_LEVEL CHAR(1),
    LOWEST_SAL NUMBER(8,2),
    HIGHEST_SAL NUMBER(8,2)
);   
INSERT INTO SAL_GRADES VALUES ('A', 1000, 2999);
INSERT INTO SAL_GRADES VALUES ('B', 3000, 5999);
INSERT INTO SAL_GRADES VALUES ('C', 6000, 9999);
INSERT INTO SAL_GRADES VALUES ('D', 10000, 14999);
INSERT INTO SAL_GRADES VALUES ('E', 15000, 24999);
INSERT INTO SAL_GRADES VALUES ('F', 25000, 40000);
*/

SELECT
    last_name
    || ' '
    || first_name emp_name,
    job_title,
    department_name,
    grade_level,
    salary
FROM
    employees
    JOIN jobs USING ( job_id )
    JOIN departments USING ( department_id )
    JOIN sal_grades ON salary BETWEEN lowest_sal AND highest_sal;
    
-- ex-10
-- Create a query to display the name and hiredate of any employee hired after employee “Davies”

-- using self join
SELECT
    e1.last_name
    || ' '
    || e1.first_name emp_name,
    e1.hire_date
FROM
    employees   e1
    JOIN employees   e2 ON e1.hire_date > e2.hire_date
                         AND e2.last_name = 'Davies';
    
    
-- using subquery
SELECT
    last_name
    || ' '
    || first_name emp_name,
    hire_date
FROM
    employees
WHERE
    hire_date > (
        SELECT
            hire_date
        FROM
            employees
        WHERE
            last_name = 'Davies'
    )
    

-- ex-11
-- Display the names and hire dates for all employees who were hired before their managers, 
-- along with their manager’s names and hiredates. 
-- Label the columns “Employee”, “Emp hired”, “Manager”, and “Manager hired” respectively.


SELECT
    emp.last_name  "Employee",
    emp.hire_date   "Emp hired",
    mgr.last_name     "Manager",
    mgr.hire_date   "Manager hired"
FROM
    employees   emp
    left JOIN employees   mgr ON emp.manager_id = mgr.employee_id
where emp.hire_date < mgr.hire_date

  
-- ex-12
-- Display the highest, lowest, sum and average salary of all employees. 
-- Label the columns “Maximum”, “Minimum”, “Sum”, and “Average” respectively.
SELECT
    MAX(salary) "Maximum",
    MIN(salary) "Minimum",
    SUM(salary) "Sum",
    AVG(nvl(salary, 0)) "Average"
FROM
    employees;
    
-- ex-13
-- Modify the above query to display the same data for each job type.

SELECT
    job_title,
    MAX(salary) "Maximum",
    MIN(salary) "Minimum",
    SUM(salary) "Sum",
    AVG(nvl(salary, 0)) "Average"
FROM
    employees
    NATURAL JOIN jobs
GROUP BY
    job_title

-- ex-14
-- Write a query to display the number of people with the same job.
SELECT
    job_title,
    COUNT(*) no_of_emps
FROM
    employees
    NATURAL JOIN jobs
GROUP BY
    job_title
ORDER BY
    no_of_emps

-- ex-15
-- Determine the number of managers without listing them. Label the column “Number of Managers”. 
-- [Hint: use the MANAGER_ID column to determine the number of managers]

SELECT
    COUNT(DISTINCT manager_id) "Number of managers"
FROM
    employees;


-- ex-16
-- Write a query that displays the difference between the highest and the lowes salaries. 
-- Label the column as “Difference”.

SELECT
    MAX(salary) - MIN(salary) "Difference"
FROM
    employees;

-- ex-17
-- Display the manager number and the salary of the lowest paid employee for that manager. 
-- Exclude anyone whose manager is not known. 
-- Exclude any group where the minimum salary is less than $6000. 
-- Sort the output in descending order of salary.

SELECT
    manager_id,
    MIN(salary) min_salary
FROM
    employees
WHERE
    manager_id IS NOT NULL
GROUP BY
    manager_id
HAVING
    MIN(salary) >= 6000
ORDER BY
    min_salary


-- ex-18
-- Write a query to display each department’s name, location, number of employees, 
-- and the average salary for all employees in that department. 
-- Label the columns “Name”, “Location”, “No.of people”, and “SAlary” respectively. 
-- Round the average salary to two decimal places.
SELECT
    department_name   "Name",
    location_id       "Location",
    COUNT(*) "No.of people",
    TO_CHAR(AVG(salary), '$9,999,990.00') "Salary"
FROM
    departments
    JOIN employees USING ( department_id )
GROUP BY
    department_name,
    location_id


-- ex-19
-- Write a query to display the lastname, and hiredate of any employee in the department as the employee “Zlotkey”. 
-- Exclude “Zlotkey”.

-- using self join
SELECT
    e1.last_name,
    e1.hire_date
FROM
    employees   e1
    JOIN employees   e2 ON e1.department_id = e2.department_id
WHERE
    e2.last_name = 'Zlotkey'
    AND e1.last_name <> 'Zlotkey'


-- using subquery
SELECT
    last_name,
    hire_date
FROM
    employees
WHERE
    last_name <> 'Zlotkey'
    AND department_id = (
        SELECT
            department_id
        FROM
            employees
        WHERE
            last_name = 'Zlotkey'
    )


-- ex-20
-- Create a query to display the employee numbers and lastnames of all employees who earn more than the average salary. 
-- Sort the result in ascending order of salary.

SELECT
    employee_id,
    last_name
FROM
    employees
WHERE
    salary > (
        SELECT
            AVG(salary)
        FROM
            employees
    )
ORDER BY
    salary


-- ex-21
-- Write a query that displays the employee number and lastname of all employees who work in a 
-- department with any employee whose lastname contains a “u”.

SELECT
    employee_id,
    last_name
FROM
    employees
WHERE
    department_id in (
        SELECT DISTINCT
            department_id
        FROM
            employees
        WHERE
            last_name LIKE '%u%'
    )


-- ex-22
-- Display the lastname, department number, and job id of all employees whose department location id is 1700.
SELECT
    last_name,
    department_id,
    job_id
FROM
    employees
    JOIN departments USING ( department_id )
WHERE
    location_id = 1700;


-- ex-23
-- Display the lastname and salary of every employee who reports to “King”.
SELECT
    last_name,
    salary
FROM
    employees
WHERE
    manager_id = any (
        SELECT
            employee_id
        FROM
            employees
        WHERE
            last_name = 'King'
    );

SELECT
    e1.last_name,
    e1.salary
FROM
    employees   e1
    JOIN employees   e2 ON e1.manager_id = e2.employee_id
                         AND e2.last_name = 'King'


-- ex-24
-- Display the department number, lastname, and job id for every employee in the “Executive” department.

-- subquery
SELECT
    department_id,
    last_name,
    job_id
FROM
    employees
WHERE
    department_id = (
        SELECT
            department_id
        FROM
            departments
        WHERE
            department_name = 'Executive'
    );

-- join
SELECT
    department_id,
    last_name,
    job_id
FROM
    employees
    JOIN departments USING ( department_id )
WHERE
    department_name = 'Executive';


-- ex-25
-- Display the employee number, lastname, and salary of all employees who earn more than the average salary 
-- and who work in a department with any employee with a “u” in their lastname.

SELECT
    employee_id,
    last_name,
    salary
FROM
    employees
WHERE
    salary > (
        SELECT
            AVG(salary)
        FROM
            employees
    )
    AND department_id IN (
        SELECT DISTINCT
            department_id
        FROM
            employees
        WHERE
            last_name LIKE '%u%'
    )

-- ex-26
-- Write a query to get unique department ID from employee table.
SELECT DISTINCT
    department_id
FROM
    employees
WHERE
    department_id IS NOT NULL;



-- ex-40 
-- Write a query to check if the first_name fields of the employees table contains numbers.
select first_name from employees
    where first_name like '%0%' or 
    first_name like '%1%' or 
    first_name like '%2%' or 
    first_name like '%3%' or 
    first_name like '%4%' or 
    first_name like '%5%' or 
    first_name like '%6%' or 
    first_name like '%7%' or 
    first_name like '%8%' or 
    first_name like '%9%';
    

-- update employees set first_name = first_name || 2 where employee_id=101;

SELECT
    first_name
FROM
    employees
WHERE
    REGEXP_LIKE ( first_name,
                  '[0-9]' )



-- ex-100
-- Write a query to display job title, employee name, and the difference between salary of the employee 
-- and minimum salary for the job.

SELECT
    j.job_title,
    e.first_name
    || ' '
    || e.last_name emp_name,
    e.salary - sq.min_salary
FROM
    employees e
    JOIN (
        SELECT
            job_id,
            MIN(salary) min_salary
        FROM
            employees
        GROUP BY
            job_id
    ) sq ON e.job_id = sq.job_id
    JOIN jobs j ON e.job_id = j.job_id


</pre>

### Day 4

<pre>
DESCRIBE employees;

DESCRIBE job_history;

SELECT
    *
FROM
    job_history
ORDER BY
    employee_id;

SELECT
    employee_id,
    job_id,
    department_id
FROM
    employees
WHERE
    employee_id IN (
        101,
        200,
        201
    )
ORDER BY
    employee_id;
    
    
    
    
    
    
    
SELECT
    employee_id,
    job_id,
    department_id,
    salary
FROM
    employees
UNION
SELECT
    employee_id,
    job_id,
    department_id,
    null
FROM
    job_history
ORDER BY
    employee_id;


-- Display the employee IDs and job IDs of those employees who currently have a job 
-- title that is the same as their previous one 
-- (that is, they changed jobs but have now gone back to doing the same job they did previously).


SELECT
    employee_id,
    job_id
FROM
    employees
INTERSECT
SELECT
    employee_id,
    job_id
FROM
    job_history
ORDER BY
    employee_id;


-- Display the employee IDs of those employees who have not changed their jobs even once.
-- using subquery:
SELECT EMPLOYEE_ID FROM EMPLOYEES WHERE EMPLOYEE_ID NOT IN (SELECT EMPLOYEE_ID FROM JOB_HISTORY);

-- USING THE MINUS OPERATOR
SELECT EMPLOYEE_ID FROM EMPLOYEES
MINUS
SELECT EMPLOYEE_ID FROM JOB_HISTORY;

SELECT MAX(EMPLOYEE_ID) FROM EMPLOYEES;


-- ADDING A NEW EMPLOYEE WITH MANDATORY FIELDS ONLY
INSERT INTO EMPLOYEES (EMPLOYEE_ID, HIRE_DATE, LAST_NAME, JOB_ID, EMAIL)
VALUES (207, '08-OCT-2010', 'SMITH', 'ST_CLERK', 'JHNSMTH');

INSERT INTO EMPLOYEES
VALUES (208, NULL, 'BORDER', 'JHNBRDR', NULL, '08-OCT-2010', 'ST_MAN', NULL, NULL, NULL, NULL);


INSERT INTO EMPLOYEES
VALUES (209, NULL, 'MARTIN', UPPER('mrtnkng'), NULL, '08-OCT-2010', 'ST_MAN', NULL, NULL, NULL, NULL);

INSERT INTO JOB_HISTORY 
SELECT EMPLOYEE_ID, '08-OCT-2010', '12-DEC-2012', JOB_ID, NULL FROM EMPLOYEES WHERE EMPLOYEE_ID=209;

COMMIT;

select sysdate from dual;

SELECT * FROM EMPLOYEES ORDER BY EMPLOYEE_ID;

SELECT * FROM JOB_HISTORY;


INSERT INTO DEPARTMENTS VALUES (280, 'DEPT-280', NULL, NULL);
INSERT INTO DEPARTMENTS VALUES (290, 'DEPT-290', NULL, NULL);
INSERT INTO DEPARTMENTS VALUES (300, 'DEPT-300', NULL, NULL);

SELECT * FROM EMPLOYEES WHERE EMPLOYEE_ID = 101;

UPDATE employees
SET
    email = 'NNKCHHR',
    salary = 17500
WHERE
    employee_id = 101;



-- UPDATE KEVIN'S (ID: 197) JOB_ID AND SALARY TO MATCH THAT OF CHARLS (ID:179)
SELECT * FROM EMPLOYEES WHERE  EMPLOYEE_ID = 197;

UPDATE EMPLOYEES
SET JOB_ID =(SELECT JOB_ID FROM EMPLOYEES WHERE EMPLOYEE_ID=179), 
    SALARY = (SELECT SALARY FROM EMPLOYEES WHERE EMPLOYEE_ID=179)
WHERE EMPLOYEE_ID = 197;

SELECT * FROM EMPLOYEES WHERE  EMPLOYEE_ID = 197;



COMMIT;

ROLLBACK;


delete from job_history where employee_id = 209;

select * from job_history;
delete from departments where department_id = 290;


update employees
set salary = 7000, first_name = 'ROBERT'
where employee_id=209;


select employee_id, first_name, last_name, salary from employees 
where employee_id=209;

COMMIT;
ROLLBACK;

CREATE TABLE TEST1(ID NUMBER);
DROP TABLE TEST1;


INSERT INTO EMPLOYEES (EMPLOYEE_ID, HIRE_DATE, LAST_NAME, JOB_ID, EMAIL)
VALUES (210, '08-OCT-2010', 'VINAY', 'SA_REP', 'VNYKMR');

SAVEPOINT A;

INSERT INTO EMPLOYEES (EMPLOYEE_ID, HIRE_DATE, LAST_NAME, JOB_ID, EMAIL)
VALUES (211, '08-OCT-2010', 'RAJESH', 'SA_REP', 'RJSHR');

SAVEPOINT B;

INSERT INTO EMPLOYEES (EMPLOYEE_ID, HIRE_DATE, LAST_NAME, JOB_ID, EMAIL)
VALUES (212, '08-OCT-2010', 'MAHESH', 'SA_REP', 'MHSHKLKRN');

SELECT * FROM EMPLOYEES WHERE EMPLOYEE_ID>209;

ROLLBACK TO B;
SELECT * FROM EMPLOYEES WHERE EMPLOYEE_ID>209;

ROLLBACK TO A;
SELECT
    *
FROM
    employees
WHERE
    employee_id > 209;
ROLLBACK;
SELECT * FROM EMPLOYEES WHERE EMPLOYEE_ID>209;

------------------------------------------------

CREATE TABLE CUSTOMERS(
    ID NUMBER,
    NAME VARCHAR(25),
    CITY VARCHAR(25) DEFAULT 'BANGALORE'
);

INSERT INTO CUSTOMERS VALUES (1, 'RAMESH KUMAR', 'CHENNAI');
INSERT INTO CUSTOMERS (ID, NAME) VALUES (2, 'HARISH RAO');
INSERT INTO CUSTOMERS VALUES (3, 'JOHN DOE', NULL);
SELECT * FROM CUSTOMERS;

DROP TABLE CUSTOMERS;
------------------------------------------------

CREATE TABLE CUSTOMERS(
    ID NUMBER PRIMARY KEY, -- COLUMN LEVEL CONSTRAINT; 2 CONSTRAINTS APPLIED- UNIQUE, NOT NULL
    NAME VARCHAR(25) NOT NULL,
    CITY VARCHAR(25) DEFAULT 'BANGALORE',
    CREATED_AT TIMESTAMP DEFAULT SYSDATE,
    MODIFIED_AT TIMESTAMP DEFAULT SYSDATE
);

INSERT INTO CUSTOMERS (ID, NAME) VALUES (1, 'VINOD');
INSERT INTO CUSTOMERS (ID, NAME) VALUES (2, 'SHYAM');
INSERT INTO CUSTOMERS (ID, NAME) VALUES (3, 'JOHN');
INSERT INTO CUSTOMERS (ID, NAME) VALUES (3, 'JOHN');

SELECT * FROM CUSTOMERS;


UPDATE CUSTOMERS SET CITY='DALLAS', MODIFIED_AT=SYSDATE WHERE ID = 3;
INSERT INTO CUSTOMERS VALUES (NULL, 'ARVIND', NULL, NULL, NULL);

SELECT COUNT(*) FROM CUSTOMERS;

DROP TABLE CUSTOMERS;
------------------------------------------------

CREATE TABLE CUSTOMERS(
    ID NUMBER,
    NAME VARCHAR(25) NOT NULL,
    CITY VARCHAR(25) DEFAULT 'BANGALORE',
    EMAIL VARCHAR(50) NOT NULL UNIQUE,
    CREATED_AT TIMESTAMP DEFAULT SYSDATE,
    MODIFIED_AT TIMESTAMP DEFAULT SYSDATE,
    
    CONSTRAINT PK_CUSTOMERS PRIMARY KEY(ID) --, -- TABLE LEVEL CONSTRAINT
    -- CONSTRAINT UNQ_CUSTOMER_EMAIL UNIQUE(EMAIL) -- MULTIPLE NULL IS ALLOWED
);

INSERT INTO CUSTOMERS (ID, NAME, EMAIL) VALUES (1, 'VINOD', 'VINOD@VINOD.CO');
INSERT INTO CUSTOMERS (ID, NAME, EMAIL) VALUES (2, 'SHYAM', 'SHYAM@EXAMPLE.COM');
INSERT INTO CUSTOMERS (ID, NAME, EMAIL) VALUES (3, 'JOHN', 'JOHN@XMPL.COM');
INSERT INTO CUSTOMERS (ID, NAME, EMAIL) VALUES (4, 'JOHN SMITH', 'JOHN@XMPL.COM');
INSERT INTO CUSTOMERS (ID, NAME, EMAIL) VALUES (5, 'PATRIC JANE', NULL);

SELECT * FROM CUSTOMERS;


------------------------------------------------------------
DROP TABLE PRODUCTS;
CREATE TABLE PRODUCTS(
    ID NUMBER PRIMARY KEY,
    NAME VARCHAR(200) NOT NULL,
    PURCHASED_PRICE NUMBER(10, 2),
    SELLING_PRICE NUMBER(10, 2),
    CONSTRAINT CHK_PRODUCTS_PURCHASED_PRICE CHECK (PURCHASED_PRICE>0),
    CONSTRAINT CHK_PRODUCTS_SELLING_PRICE CHECK (SELLING_PRICE>0),
    CONSTRAINT CHK_PRODUCTS_MIN_SELLING_PRICE CHECK (SELLING_PRICE>=PURCHASED_PRICE)
);

INSERT INTO PRODUCTS VALUES (1, 'DELL OPTICAL MOUSE', 980, 1200);
SELECT * FROM PRODUCTS;
INSERT INTO PRODUCTS VALUES (2, 'TVS MOUSE', 900, 530);

---------------------------------------------------------------------------

DROP TABLE PRODUCTS;
DROP TABLE CATEGORIES;

CREATE TABLE CATEGORIES(
    CATEGORY_ID NUMBER(4) PRIMARY KEY,
    CATEGORY_NAME VARCHAR(20) NOT NULL,
    DESCRIPTION VARCHAR(50)
);
CREATE TABLE PRODUCTS(
    ID NUMBER PRIMARY KEY,
    NAME VARCHAR(30) NOT NULL,
    PRICE NUMBER(10, 2),
    CATEGORY_ID NUMBER(4), -- REFERENCES CATEGORIES(CATEGORY_ID),
    CONSTRAINT CHK_PRODUCTS_SELLING_PRICE CHECK (PRICE>0),
    CONSTRAINT FK_PRODUCTS_CATEGORY_ID FOREIGN KEY (CATEGORY_ID) 
        REFERENCES CATEGORIES(CATEGORY_ID)
        ON DELETE CASCADE --SET NULL
);
INSERT INTO CATEGORIES VALUES (1, 'HOME APPLIANCES', 'DAY TO DAY PRODUCTS USED AT HOME');
INSERT INTO CATEGORIES VALUES (2, 'COMPUTERS', 'GREAT DEALS ON COMPUTERS AND LAPTOPS (BRANDED)');
INSERT INTO PRODUCTS VALUES (1, 'PHILIPS COFFE MAKER', 1850, 1);
INSERT INTO PRODUCTS VALUES (2, 'AMAZON AIR PURIFIER', 12500, 1);
INSERT INTO PRODUCTS VALUES (3, 'DELL INSPIRON 5500', 124850, 2);

SELECT * FROM CATEGORIES;
SELECT * FROM PRODUCTS;

-- VIOLATES FOREIGN KEY CONSTRAINT - NO PARENT KEY 7
INSERT INTO PRODUCTS VALUES (4, 'APEX EXTERIOR PAINT', 450, 7);
-- VIOLATES FOREIGN KEY CONSTRAINT - CHILD RECORDS EXIST
DELETE FROM CATEGORIES WHERE CATEGORY_ID=2;



-- EXAMPLE FOR COMPOSITE PRIMARY KEY

-- ORDERS TABLE (RECORDS THE DETAILS OF ORDER PLACED BY CUSTOMER)
CREATE TABLE CUSTOMER_ORDERS(
    ORDER_ID NUMBER(10)PRIMARY KEY,
    CUSTOMER_ID NUMBER NOT NULL REFERENCES CUSTOMERS, -- CUSTOMERS(ID)
    ORDER_DATE TIMESTAMP DEFAULT SYSDATE,
    SHIP_ADDRESS VARCHAR(100)
);

INSERT INTO CUSTOMER_ORDERS (ORDER_ID, CUSTOMER_ID) VALUES (20012, 1);
INSERT INTO CUSTOMER_ORDERS (ORDER_ID, CUSTOMER_ID) VALUES (20123, 2);

-- TABLE WITH COMPOSITE PRIMARY KEY (PRIMARY KEY CONSTRAINT ON MULTIPLE COLUMNS TOGETHER)
CREATE TABLE LINE_ITEMS(
    ORDER_ID NUMBER(10) NOT NULL REFERENCES CUSTOMER_ORDERS,
    PRODUCT_ID NUMBER NOT NULL REFERENCES PRODUCTS,
    PRICE NUMBER(10,2) CHECK (PRICE>0),
    QUANTITY NUMBER CHECK (QUANTITY>0),
    DISCOUNT NUMBER(5,2) CHECK (DISCOUNT>=0),
    CONSTRAINT PK_LINEITEMS_ORDERID_PRODUCTID PRIMARY KEY (ORDER_ID, PRODUCT_ID)
);

INSERT INTO LINE_ITEMS VALUES (20012, 1, 1850, 1, 0);
INSERT INTO LINE_ITEMS VALUES (20012, 2, 12000, 1, 0);
INSERT INTO LINE_ITEMS VALUES (20012, 2, 123, 10, .50); -- ERROR COMPOSITE PRIMARY KEY CONSTRAINT VIOLATION


SELECT * FROM LINE_ITEMS;

-- ALTER TABLE EXAMPLES

ALTER TABLE CUSTOMERS READ ONLY;
ALTER TABLE CUSTOMERS READ WRITE;
ALTER TABLE CUSTOMERS ADD PHONE VARCHAR(15);
ALTER TABLE CUSTOMERS MODIFY PHONE VARCHAR(20);
ALTER TABLE CUSTOMERS MODIFY EMAIL VARCHAR(25);

INSERT INTO CUSTOMERS (ID, NAME, EMAIL) VALUES (
(SELECT MAX(ID)+1 FROM CUSTOMERS), 'MAHESH IYER', 'MSHYR@XMPL.COM');

ALTER TABLE CUSTOMERS MODIFY CITY DEFAULT 'BENGALURU';

ALTER TABLE CUSTOMERS DROP COLUMN MODIFIED_AT;
ALTER TABLE CUSTOMERS RENAME COLUMN CREATED_AT TO CREATED_TIMESTAMP;
ALTER TABLE LINE_ITEMS DROP PRIMARY KEY;

ALTER TABLE LINE_ITEMS ADD CONSTRAINT PK_LINEITEMS_ORDERID_PRODUCTID PRIMARY KEY(ORDER_ID, PRODUCT_ID);
ALTER TABLE CUSTOMERS ADD CONSTRAINT UNQ_PHONE UNIQUE(PHONE);


CREATE SEQUENCE SEQ_CUSTOMERS_ID START WITH 6;

INSERT INTO CUSTOMERS (ID, NAME, EMAIL) VALUES (SEQ_CUSTOMERS_ID.NEXTVAL, 'KRISHNA', 'KRISHNA@XMPL.COM');
SELECT * FROM CUSTOMERS;

SELECT SEQ_CUSTOMERS_ID.NEXTVAL FROM DUAL;
SELECT SEQ_CUSTOMERS_ID.CURRVAL FROM DUAL;



-- find the first and the last record in the table
select * from products where rowid in (
    (select min(rowid) from products), 
    (select max(rowid) from products));
    
-- exercise: list top 3 salaried employees 
-- modifiction: list top 3 salaried employees in each department (name of the department along with emp details)

</pre>

### Day 5

<pre>
SET SERVEROUTPUT ON;

DECLARE
    TYPE empl_type IS RECORD (
        emp_name    VARCHAR(45),
        dept_name   departments.department_name%TYPE,
        city        locations.city%TYPE,
        salary      employees.salary%TYPE
    );
    e1 empl_type;
BEGIN
    SELECT
        first_name
        || ' '
        || last_name,
        department_name,
        city,
        salary
    INTO e1
    FROM
        employees
        JOIN departments USING ( department_id )
        JOIN locations USING ( location_id )
    WHERE
        employee_id = 102;

    dbms_output.put_line('EMPLOYEE NAME = ' || e1.emp_name);
    dbms_output.put_line('DEPARTMENT    = ' || e1.dept_name);
    dbms_output.put_line('CITY          = ' || e1.city);
    dbms_output.put_line('SALARY        = $' || e1.salary);
END;


DECLARE
    TYPE emp_rec_type IS RECORD (
        id       NUMBER,
        name     VARCHAR(40),
        salary   NUMBER(10, 2)
    );
    TYPE emps_type IS TABLE OF emp_rec_type INDEX BY VARCHAR(50);
    e1     emp_rec_type;
    e2     emp_rec_type;
    e3     emp_rec_type;
    emps   emps_type;
    
    email varchar(50);
    
BEGIN
    SELECT 12, 'John doe', 23000 INTO e1 FROM dual;
    SELECT 56, 'John smith', 35000 INTO e2 FROM dual;
    emps('john@exmaple.com') := e1;
    emps('jsmith@exmaple.com') := e2;
    select 22, 'John Smith Jr.', 26000 into emps('jsmith@xmpl.com') from dual; -- VALUE CAN BE DUPLICATE
    select 22, 'John Smith Jr.', 26000 into emps('jsmithjr@xmpl.com') from dual; -- VALUE CAN BE DUPLICATE
    select 99, 'Jerry Smith', 55000 into emps('jsmithjr@xmpl.com') from dual; -- key CAN NOT BE DUPLICATE; overwrites the existing value
    dbms_output.put_line('emps.count = ' || emps.COUNT);
    e3 := emps('john@exmaple.com');
    dbms_output.put_line(e3.id || ', ' || e3.name || ', ' || e3.salary);
    email := emps.NEXT('john@exmaple.com');
    dbms_output.put_line('email is ' || email);
    e3 := emps(email);
    dbms_output.put_line(e3.id || ', ' || e3.name || ', ' || e3.salary);
    email := emps.first;
    loop
        e3 := emps(email);
        dbms_output.put_line(e3.id || ', ' || e3.name || ', ' || e3.salary);
        email := emps.next(email);
        exit when email is null;
    end loop;
END;


DECLARE
    CURSOR c1 IS
    SELECT
        first_name,
        last_name,
        salary
    FROM
        employees
    WHERE
        job_id = 'IT_PROG';

    v_first_name   employees.first_name%TYPE;
    v_last_name    employees.last_name%TYPE;
    v_salary       employees.salary%TYPE;
BEGIN
    
    -- OPEN THE CURSOR
    OPEN c1; -- SQL QUERY IS EXECUTED AT THIS POINT IN TIME
    
    
    LOOP
        FETCH c1 INTO
            v_first_name,
            v_last_name,
            v_salary; -- ATTEMPT TO FETCH DATA FROM CURSOR'S CURRENT ROW
            
        -- c1%found will be true if fetch was successful; else c1%found is false
        -- c1%notfound will be false if fetch was successful; else c1%notfound is true
        
        EXIT WHEN c1%notfound;
        dbms_output.put_line(v_first_name || ' ' || v_last_name || ' earns $' || v_salary || ' per month');
        
        dbms_output.put_line('c1%rowcount (no.of rows fetched so far) is ' || c1%rowcount);
    END LOOP;

    CLOSE c1; -- RELEASE RESOURCES HELD BY THE CURSOR (LIKE C/C++ POINTERS)
END;


DECLARE
    CURSOR c1 IS
    SELECT
        first_name,
        last_name,
        salary
    FROM
        employees
    WHERE
        job_id = 'IT_PROG';

BEGIN

    

    dbms_output.put_line('before for loop, c1%isopen is ' || case when c1%isopen then 'true' else 'false' end);
    -- when the loop begins, open c1 is done and then fetch c1 into e1 also is done
    for e1 in c1
    LOOP
        -- dbms_output.put_line('inside for loop, c1%isopen is ' || case when c1%isopen then 'true' else 'false' end);
        -- dbms_output.put_line('c1%rowcount is ' || c1%rowcount);
        dbms_output.put_line(c1%rowcount || '. ' || e1.first_name || ' ' || e1.last_name || ' earns $' || e1.salary || ' per month');
    END LOOP;
    -- when the loop exits, close c1 alos is done
    dbms_output.put_line('after for loop, c1%isopen is ' || case when c1%isopen then 'true' else 'false' end);
END;


begin
    for e1 in (select * from employees where salary>=15000) -- anonymous cursor
    loop
        dbms_output.put_line(e1.employee_id || '. ' || e1.first_name || ' ' || e1.last_name || ' earns $' || e1.salary || ' per month');
    end loop;
end;


declare
    cursor c1(v_job_id employees.job_id%type) is select * from employees where job_id = v_job_id;
    e1 employees%rowtype;
begin
    open c1('IT_PROG');
    loop 
        fetch c1 into e1;
        exit when c1%notfound;
        dbms_output.put_line(e1.employee_id || '. ' || e1.first_name || ' ' || e1.last_name || ' earns $' || e1.salary || ' per month');
    end loop;
    close c1;
    
    dbms_output.put_line('--------------');
    open c1('SA_REP');
    loop 
        fetch c1 into e1;
        exit when c1%notfound;
        dbms_output.put_line(e1.employee_id || '. ' || e1.first_name || ' ' || e1.last_name || ' earns $' || e1.salary || ' per month');
    end loop;
    close c1;
end;


declare
    cursor c1(v_job_id employees.job_id%type) is select * from employees where job_id = v_job_id;
begin
    for e1 in c1('IT_PROG')
    loop 
        dbms_output.put_line(e1.employee_id || '. ' || e1.first_name || ' ' || e1.last_name || ' earns $' || e1.salary || ' per month');
    end loop;
    
    dbms_output.put_line('--------------');
    for e1 in c1('SA_REP')
    loop 
        dbms_output.put_line(e1.employee_id || '. ' || e1.first_name || ' ' || e1.last_name || ' earns $' || e1.salary || ' per month');
    end loop;
end;



declare
    v_fname employees.first_name%type := 'Vinod'; -- 'Neena', 'John'
    v_lname employees.last_name%type;
begin
    dbms_output.put_line('start of pl/sql execution');
    select first_name into v_lname
        from employees
        where first_name = v_fname;
        
    dbms_output.put_line('Hello, ' || v_lname);
    
    -- more sql statements
    dbms_output.put_line('end of pl/sql execution'); -- will not be printed when there is an exception raised
    
exception
    when no_data_found then
        dbms_output.put_line('No data found with firstname: ' || v_fname);
    when too_many_rows then
        dbms_output.put_line('More than one record found with firstname ' || v_fname);
end;



declare
    v_fname employees.first_name%type := 'Vinod'; -- 'Neena', 'John'
    v_lname employees.last_name%type;
begin
    dbms_output.put_line('start of pl/sql execution');
    
    begin
        select first_name into v_lname
            from employees
            where first_name = v_fname;
            
        dbms_output.put_line('Hello, ' || v_lname);
    exception
        when no_data_found then
            dbms_output.put_line('No data found with firstname: ' || v_fname);
        when too_many_rows then
            dbms_output.put_line('More than one record found with firstname ' || v_fname);
    end;    
    -- more sql statements
    dbms_output.put_line('end of pl/sql execution');
    
exception
    when others then
        dbms_output.put_line('OOPS! some error occured!');
end;


select * from customers;
insert into customer_orders values(9001, 9, sysdate, 'ISRO lyt, Bangalore');


DECLARE
    -- declare an exception variable
    PARENT_KEY_NOT_FOUND EXCEPTION;
    -- associate the above user defined exception with oracle error code '-02291'
    PRAGMA EXCEPTION_INIT(PARENT_KEY_NOT_FOUND, -2291);
BEGIN
    insert into job_history values (109, '20-JAN-1998', '31-MAR-2001', 'LIB_CLERK', 300);
    dbms_output.put_line('Data inserted successfully');
    
EXCEPTION
    WHEN PARENT_KEY_NOT_FOUND THEN
        dbms_output.put_line('FOREIGN KEY VIOLATION; PARENT DOES NOT EXIST');
        dbms_output.put_line('ORACLE ERROR CODE ' || SQLCODE);
        dbms_output.put_line('ORACLE ERROR MSSG ' || SQLERRM);
END;


-- CREATE A STORED PROCEDURE TO ACCEPT NAME, EMAIL, CITY AND PHONE.
-- IF THERE IS CUSTOMER RECORD WITH THE GIVEN EMAIL, THEN IT SHOULD UPDATE THE NAME/CITY/PHONE OF THE SAME CUSTOMER
-- OTHERWISE, IT SHOULD ADD A NEW CUSTOMER, WITH THE DATA GIVEN.
CREATE OR REPLACE PROCEDURE ADD_OR_UPDATE_CUSTOMER(
    P_NAME CUSTOMERS.NAME%TYPE,
    P_CITY CUSTOMERS.CITY%TYPE,
    P_EMAIL CUSTOMERS.EMAIL%TYPE,
    P_PHONE CUSTOMERS.PHONE%TYPE
) IS
-- DECLARATION SECTION
    V_CUSTOMER_COUNT NUMBER;
    V_NEW_ID CUSTOMERS.ID%TYPE;
BEGIN
-- EXECUTION SECTION
    SELECT COUNT(*) INTO V_CUSTOMER_COUNT
        FROM CUSTOMERS 
        WHERE UPPER(EMAIL) = UPPER(P_EMAIL);
    
    IF V_CUSTOMER_COUNT=0 THEN
        SELECT MAX(ID)+1 INTO V_NEW_ID FROM CUSTOMERS;
        INSERT INTO CUSTOMERS VALUES (V_NEW_ID, P_NAME, P_CITY, P_EMAIL, SYSDATE, P_PHONE);
    ELSE
        UPDATE CUSTOMERS SET NAME=P_NAME, CITY=P_CITY, PHONE=P_PHONE WHERE EMAIL=P_EMAIL;
    END IF;
    
    COMMIT;
END;
/

select * from customers;

begin
    add_or_update_customer('PRANAV KUMAR', 'VASCO-DA-GAMMA', 'PRNVKMR@GMAIL.COM', '9876576000');
end;


EXECUTE add_or_update_customer('PRANAV KUMAR', 'VASCO-DA-GAMMA', 'PRNVKMR@GMAIL.COM', '9876576000')


create or replace function net_salary(p_salary employees.salary%type) return number is
    v_pf employees.salary%type; -- deduction 12% of sal
    v_hra employees.salary%type; -- addition 20% sal
    v_tds employees.salary%type; -- deduction 10% sal
    v_netsal employees.salary%type;
begin
    v_pf := p_salary * .12;
    v_hra := p_salary * .2;
    v_tds := p_salary * .1;
    v_netsal := p_salary - v_pf - v_tds + v_hra;
    return v_netsal;
end;

SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, SALARY, NET_SALARY(SALARY) AS NET_SALARY
FROM EMPLOYEES
WHERE SALARY > 8000;

DECLARE
    NETSAL NUMBER(10,2);
BEGIN
    NETSAL := NET_SALARY(12500);
    DBMS_OUTPUT.PUT_LINE('NET SALARY FOR 12500 IS ' || NETSAL);
END;

</pre>

### Day 6

<pre>
create or replace procedure employee_count is
    EMP_COUNT NUMBER;
begin
    SELECT COUNT(*) INTO EMP_COUNT FROM EMPLOYEES;
    dbms_output.put_line('TOTAL EMPLOYEES: ' || EMP_COUNT);
end;

SET SERVEROUTPUT ON;
EXEC EMPLOYEE_COUNT;


DROP PROCEDURE EMPLOYEE_COUNT;

CREATE OR REPLACE FUNCTION EMPLOYEE_COUNT RETURN NUMBER IS
    EMP_COUNT NUMBER;
begin
    SELECT COUNT(*) INTO EMP_COUNT FROM EMPLOYEES;
    RETURN EMP_COUNT;
end;

SELECT EMPLOYEE_COUNT FROM DUAL;

DECLARE
    EC NUMBER;
BEGIN
    EC := EMPLOYEE_COUNT;
    DBMS_OUTPUT.PUT_LINE('TOTAL EMPS = ' || EMPLOYEE_COUNT);
    DBMS_OUTPUT.PUT_LINE('TOTAL EMPS = ' || EC);
END;


CREATE OR REPLACE PROCEDURE GET_EMP_DATA(
    P_EMPLOYEE_ID IN NUMBER, 
    P_EMP_NAME OUT VARCHAR,
    P_SALARY OUT NUMBER,
    P_DEPARTMENT_NAME OUT VARCHAR,
    P_JOB_TITLE OUT VARCHAR )  IS
BEGIN
    SELECT FIRST_NAME || ' ' || LAST_NAME,
        SALARY, DEPARTMENT_NAME, JOB_TITLE
        INTO P_EMP_NAME, P_SALARY, P_DEPARTMENT_NAME, P_JOB_TITLE
        FROM EMPLOYEES
        JOIN DEPARTMENTS USING(DEPARTMENT_ID)
        JOIN JOBS USING(JOB_ID)
        WHERE EMPLOYEE_ID = P_EMPLOYEE_ID;
END;

VARIABLE name VARCHAR2(50);
VARIABLE sal NUMBER;
VARIABLE dept VARCHAR2(100);
VARIABLE jobt VARCHAR2(100);

SELECT :name, :sal, :dept, :jobt FROM dual;
EXEC get_emp_data(109, :name, :sal, :dept, :jobt);
SELECT :name, :sal, :dept, :jobt FROM dual;


-- change the job of an employee along with department and salary
-- parameters to the proc are - employee_id, new_job_id, new_department_id, new_salary

select * from job_history where employee_id = 115;

CREATE OR REPLACE PROCEDURE CHANGE_EMP_JOB(
    P_EMPLOYEE_ID EMPLOYEES.EMPLOYEE_ID%TYPE,
    P_JOB_ID EMPLOYEES.JOB_ID%TYPE,
    P_DEPARTMENT_ID EMPLOYEES.DEPARTMENT_ID%TYPE,
    P_SALARY EMPLOYEES.SALARY%TYPE) IS
    
    V_JOB_ID EMPLOYEES.JOB_ID%TYPE;
    V_DEPARTMENT_ID EMPLOYEES.DEPARTMENT_ID%TYPE;
    V_START_DATE DATE;
    V_SALARY EMPLOYEES.SALARY%TYPE;
    
    FK_EXCEPTION EXCEPTION;
    PRAGMA EXCEPTION_INIT(FK_EXCEPTION, -2291);
    V_JOB_COUNT NUMBER;
    INVALID_JOB_ID EXCEPTION;
BEGIN
    SELECT JOB_ID, DEPARTMENT_ID, HIRE_DATE, SALARY
        INTO V_JOB_ID, V_DEPARTMENT_ID, V_START_DATE, V_SALARY
        FROM EMPLOYEES
        WHERE EMPLOYEE_ID = P_EMPLOYEE_ID;
        
    SELECT COUNT(*)
        INTO V_JOB_COUNT
        FROM JOBS
        WHERE JOB_ID = P_JOB_ID;
        
    IF V_JOB_COUNT=0 THEN
        RAISE INVALID_JOB_ID;
    END IF;
    
    IF P_SALARY < V_SALARY THEN
        RAISE_APPLICATION_ERROR(-20003, 'SALARY MUST BE >=' || V_SALARY);
    END IF;
    
    UPDATE EMPLOYEES
        SET JOB_ID = P_JOB_ID,
        DEPARTMENT_ID = P_DEPARTMENT_ID,
        SALARY = P_SALARY
        WHERE EMPLOYEE_ID = P_EMPLOYEE_ID;
        
-- THE HR DB HAS A TRIGGER THAT ADDS A NEW ROW IN THE JOB_HISTORY WHEN A RECORD
-- IN THE EMPLOYEES TABLE IS UPDATED WITH JOB_ID OR DEPARTMENT_ID

-- BECAUSE OF THE ABOVE, THE STATEMENT BELOW IS CAUSING PRIMARY-KEY VIOLATION.

--    INSERT INTO JOB_HISTORY 
--        VALUES (P_EMPLOYEE_ID, V_START_DATE, SYSDATE, V_JOB_ID, V_DEPARTMENT_ID);
    COMMIT;
EXCEPTION
    WHEN INVALID_JOB_ID THEN
        RAISE_APPLICATION_ERROR(-20000, 'INVALID JOB ID: ' || P_JOB_ID);
    WHEN FK_EXCEPTION THEN
        RAISE_APPLICATION_ERROR(-20001, 'INVALID DEPARTMENT ID: ' || P_DEPARTMENT_ID);
    WHEN NO_DATA_FOUND THEN
        RAISE_APPLICATION_ERROR(-20002, 'NO RECORD FOUND FOR EMPLOYEE WITH ID ' || P_EMPLOYEE_ID);
END;


EXEC CHANGE_EMP_JOB(116, 'ST_MAN', 50, 5500);
SELECT * FROM JOB_HISTORY WHERE EMPLOYEE_ID = 116;
SELECT * FROM EMPLOYEES WHERE EMPLOYEE_ID=116;

INSERT INTO JOB_HISTORY 
VALUES (115, '18-05-03', SYSDATE, 'PU_CLERK', 30);


UPDATE EMPLOYEES SET SALARY=5000 WHERE EMPLOYEE_ID=116;
COMMIT;


-- EACH TIME A RECORD IN CUSTOMERS TABLE IS UPDATED, A NEW ROW WILL BE
-- INSERTED WITH FEW DETAILS (REF COLUMN LIST)
CREATE TABLE CUSTOMRS_UPDATE_HISTORY(
    UPDATED_ON TIMESTAMP,
    UPDATED_BY VARCHAR(25),
    ID NUMBER,
    NAME VARCHAR(25),
    CITY VARCHAR(25),
    EMAIL VARCHAR(25),
    PHONE VARCHAR(25)
);

CREATE OR REPLACE TRIGGER TR_CUSTOMRS_UPDATE_HISTORY
BEFORE UPDATE ON CUSTOMERS
FOR EACH ROW
BEGIN
    INSERT INTO CUSTOMRS_UPDATE_HISTORY
        VALUES (SYSDATE, USER, :OLD.ID, :OLD.NAME, :OLD.CITY, :OLD.EMAIL, :OLD.PHONE);
END;

SELECT * FROM CUSTOMERS;
SELECT * FROM CUSTOMRS_UPDATE_HISTORY;


UPDATE CUSTOMERS SET CITY='SHIVAMOGGA' WHERE ID = 2;
UPDATE CUSTOMERS SET PHONE='9988776655' WHERE ID = 2;
UPDATE CUSTOMERS SET CITY =INITCAP(CITY);

CREATE TABLE HR_TABLE_DML_HISTORY(
    TABLE_NAME VARCHAR(30),
    DML_TYPE VARCHAR(10), -- INSERT/UPDATE/DELETE
    UPDATED_ON TIMESTAMP,
    UPDATED_BY VARCHAR(10)
);

CREATE OR REPLACE TRIGGER TR_HR_TABLE_INSERT_HISTORY
AFTER INSERT 
ON CUSTOMERS
BEGIN
    INSERT INTO HR_TABLE_DML_HISTORY VALUES ('CUSTOMERS', 'INSERT', SYSDATE, USER);
END;

CREATE OR REPLACE TRIGGER TR_HR_TABLE_UPDATE_HISTORY
AFTER UPDATE 
ON CUSTOMERS
BEGIN
    INSERT INTO HR_TABLE_DML_HISTORY VALUES ('CUSTOMERS', 'UPDATE', SYSDATE, USER);
END;

CREATE OR REPLACE TRIGGER TR_HR_TABLE_DELETE_HISTORY
AFTER DELETE 
ON CUSTOMERS
BEGIN
    INSERT INTO HR_TABLE_DML_HISTORY VALUES ('CUSTOMERS', 'DELETE', SYSDATE, USER);
END;


SELECT * FROM HR_TABLE_DML_HISTORY;

UPDATE CUSTOMERS SET EMAIL=LOWER(EMAIL);
DELETE CUSTOMERS WHERE PHONE IS NULL;


SELECT FIRST_NAME, LAST_NAME, SALARY FROM EMPLOYEES WHERE EMPLOYEE_ID = 117;

UPDATE EMPLOYEES SET SALARY = 3000 WHERE EMPLOYEE_ID=117;

CREATE OR REPLACE TRIGGER TR_CHECK_SAL_ON_UPDATE_OF_EMP
BEFORE UPDATE OF SALARY
ON EMPLOYEES
FOR EACH ROW
WHEN (OLD.SALARY>NEW.SALARY)
BEGIN
    -- INSIDE BEGIN-END BLOCK YOU MUST USE COLON PREFIX WITH OLD/NEW (EX :OLD AND :NEW)
    RAISE_APPLICATION_ERROR(-20004, 'WHEN UPDATING, SALARY CANNOT BE LESS THAN CURRENT SALARY');
END;

-- A NEW PACKAGE SPECIFICATION CALLED "VND"
CREATE OR REPLACE PACKAGE VND IS
    
    FUNCTION GET_NET_SAL(P_SALARY NUMBER) RETURN NUMBER;
    
    PROCEDURE GET_EMP_DATA(
        P_EMPLOYEE_ID IN NUMBER, 
        P_EMP_NAME OUT VARCHAR,
        P_SALARY OUT NUMBER,
        P_DEPARTMENT_NAME OUT VARCHAR,
        P_JOB_TITLE OUT VARCHAR );
END;


CREATE OR REPLACE PACKAGE BODY VND IS

    FUNCTION GET_NET_SAL(P_SALARY NUMBER) RETURN NUMBER IS
    BEGIN
        RETURN P_SALARY * (1 + .25 - 0.10 - 0.12);
    END;

    PROCEDURE GET_EMP_DATA(
        P_EMPLOYEE_ID IN NUMBER, 
        P_EMP_NAME OUT VARCHAR,
        P_SALARY OUT NUMBER,
        P_DEPARTMENT_NAME OUT VARCHAR,
        P_JOB_TITLE OUT VARCHAR )  IS
    BEGIN
        SELECT FIRST_NAME || ' ' || LAST_NAME,
            SALARY, DEPARTMENT_NAME, JOB_TITLE
            INTO P_EMP_NAME, P_SALARY, P_DEPARTMENT_NAME, P_JOB_TITLE
            FROM EMPLOYEES
            JOIN DEPARTMENTS USING(DEPARTMENT_ID)
            JOIN JOBS USING(JOB_ID)
            WHERE EMPLOYEE_ID = P_EMPLOYEE_ID;
    END;
END;


SELECT VND.GET_NET_SAL(2400) FROM DUAL;
SELECT FIRST_NAME, LAST_NAME, SALARY, VND.GET_NET_SAL(SALARY) FROM EMPLOYEES;

VARIABLE name VARCHAR2(50);
VARIABLE sal NUMBER;
VARIABLE dept VARCHAR2(100);
VARIABLE jobt VARCHAR2(100);

SELECT :name, :sal, :dept, :jobt FROM dual;
EXEC VND.get_emp_data(109, :name, :sal, :dept, :jobt);
SELECT :name, :sal, :dept, :jobt FROM dual;

-- TOP N ANALYSIS QUERIES

-- 1. TOP EARNING EMPLOYEE
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, DEPARTMENT_ID, SALARY FROM EMPLOYEES
WHERE SALARY = (SELECT MAX(SALARY) FROM EMPLOYEES);

-- 2. TOP 5 SALARIED EMPLOYEES
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, DEPARTMENT_ID, SALARY FROM EMPLOYEES EMP_OUTER
WHERE 4 >= (SELECT COUNT(*) FROM EMPLOYEES WHERE SALARY>EMP_OUTER.SALARY)
ORDER BY SALARY DESC;

-- 3. TOP 5 RANKED (BY SALARY) EMPLOYEES
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, DEPARTMENT_ID, SALARY FROM EMPLOYEES EMP_OUTER
WHERE 9 >= (SELECT COUNT(DISTINCT SALARY) FROM EMPLOYEES WHERE SALARY>EMP_OUTER.SALARY)
ORDER BY SALARY DESC;

-- 4. TOP 3 RANKED (BY SALARY) EMPLOYEES IN THEIR RESPECTIVE DEPARTMENTS
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMP_OUTER.DEPARTMENT_ID, DEPARTMENT_NAME, SALARY FROM EMPLOYEES EMP_OUTER
JOIN DEPARTMENTS ON EMP_OUTER.DEPARTMENT_ID=DEPARTMENTS.DEPARTMENT_ID
WHERE 3 > (
    SELECT COUNT(DISTINCT SALARY) FROM EMPLOYEES 
    WHERE SALARY>EMP_OUTER.SALARY 
    AND DEPARTMENT_ID=EMP_OUTER.DEPARTMENT_ID)
ORDER BY DEPARTMENT_NAME, SALARY DESC;

-- 5. TOP 3 RANKED (BY SALARY) EMPLOYEES IN THEIR RESPECTIVE JOB TITLES (A SMALL EXERCISE)
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, JOB_TITLE, SALARY FROM EMPLOYEES EMP_OUTER
JOIN JOBS ON EMP_OUTER.JOB_ID=JOBS.JOB_ID
WHERE 3 > (
    SELECT COUNT(DISTINCT SALARY) FROM EMPLOYEES 
    WHERE SALARY>EMP_OUTER.SALARY 
    AND JOB_ID=EMP_OUTER.JOB_ID)
ORDER BY JOB_TITLE, SALARY DESC;

-- 6. RANK EMPLOYEES BASED ON SALARY
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, SALARY, DENSE_RANK() OVER (ORDER BY SALARY DESC) EMP_RANK
FROM EMPLOYEES;

-- 7. EMPLOYEES SAME OR ABOVE RANK 5
SELECT * FROM (
    SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, SALARY, DENSE_RANK() OVER (ORDER BY SALARY DESC) EMP_RANK
    FROM EMPLOYEES) 
WHERE EMP_RANK <= 5;

-- 8. RANK EMPLOYEES WITH IN EACH DEPARTMENT, BASED ON SALARY
SELECT E.EMPLOYEE_ID, E.FIRST_NAME, E.LAST_NAME, E.DEPARTMENT_ID, DEPARTMENT_NAME, SALARY, 
DENSE_RANK() OVER (PARTITION BY E.DEPARTMENT_ID ORDER BY SALARY DESC) EMP_RANK
FROM EMPLOYEES E
JOIN DEPARTMENTS D ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
ORDER BY E.DEPARTMENT_ID, SALARY DESC;

-- 9. DISPLAY LIST OF TOP 3 EMPLOYEES BASED ON SALARY IN THEIR RESPECTIVE DEPARTMENTS
SELECT * FROM (
    SELECT E.EMPLOYEE_ID, E.FIRST_NAME, E.LAST_NAME, E.DEPARTMENT_ID, DEPARTMENT_NAME, SALARY, 
    DENSE_RANK() OVER (PARTITION BY E.DEPARTMENT_ID ORDER BY SALARY DESC) EMP_RANK
    FROM EMPLOYEES E
    JOIN DEPARTMENTS D ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
    ORDER BY E.DEPARTMENT_ID, SALARY DESC) 
WHERE EMP_RANK<=3
ORDER BY DEPARTMENT_NAME, SALARY DESC;


SELECT * FROM (
    SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, DEPARTMENT_ID, SALARY, 
    DENSE_RANK() OVER (PARTITION BY DEPARTMENT_ID ORDER BY SALARY DESC) EMP_RANK
    FROM EMPLOYEES
    ORDER BY DEPARTMENT_ID, SALARY DESC) 
NATURAL JOIN DEPARTMENTS
WHERE EMP_RANK<=3
ORDER BY DEPARTMENT_ID, SALARY DESC;

-- NEW IN ORACLE 12C ONWARDS --> FETCH & OFFSET
-- TOP 5 SALARIED EMPLOYEES
SELECT * FROM EMPLOYEES ORDER BY SALARY DESC FETCH NEXT 5 ROWS ONLY;

SELECT * FROM EMPLOYEES WHERE SALARY IN (SELECT DISTINCT SALARY
FROM EMPLOYEES ORDER BY SALARY DESC FETCH NEXT 5 ROWS ONLY);

-- 5TH HIGHEST EARNING EMPLOYEE
SELECT * FROM EMPLOYEES ORDER BY SALARY DESC
OFFSET 4 ROWS FETCH NEXT 1 ROWS ONLY;

</pre>
