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
    V_EMPLOYEE_ID EMPLOYEE.EMPLOYEE_ID%TYPE := 102;
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





</pre>