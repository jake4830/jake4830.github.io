
==============================================================
7장 명시적 커서 사용 ( 여러 행 처리하는 방법)
==============================================================

명시적 커서 : 프로그래머에 의해 선언되고 사용되는 커서 
             목적 : PLSQL 블럭내에서 여러행을 처리하기 위한 방법
      1) 선언 : 선언부 
               CURSOR emp_cur IS Select (여러행 가져오는 select 문)
    
      2) open : OPEN emp_cur;   정의한 select  문이 수행된다.
         loop
      3) fetch : FETCH emp_cur INTO a, b;
         exit when emp_cur%notfound;
         end loop;
      4) close  : CLOSE emp_cur;

-- cursor 사용1 : BASIC LOOP
declare
   CURSOR emp_cur IS 
       select ename, sal from emp where deptno = 20;
  v_ename   emp.ename%type;
  v_sal     emp.sal%type;
begin 
  OPEN EMP_CUR;
  LOOP 
     FETCH emp_cur INTO v_ename, v_sal;
     dbms_output.put_line(v_ename || '  '|| v_sal);
     EXIT WHEN emp_cur%notfound;
  END LOOP;
  CLOSE EMP_CUR;
end;
/


-- cursor 사용2 : CURSOR FOR LOOP