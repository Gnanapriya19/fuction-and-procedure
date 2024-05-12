Tables used: 
SQL> select * from ititems; 
ITEMID ACTUALPRICE ORDID PRODID 
--------- ----------- -------- --------- 
101	2000 500 201 
102	3000 1600 202 
103	4000 600 202 
 
Program For General Procedure – Selected Record‘S Price Is Incremented By 500 , 
Executing The Procedure Created And Displaying The Updated Table 
SQL> create procedure itsum(identity number, total number) is price number; 
2	null_price exception; 
3	begin 
4	select actualprice into price from ititems where itemid=identity; 
5	if price is null then 
6	raise null_price; 
7	else 
8	update ititems set actualprice=actualprice+total where itemid=identity;  9 end if; 
10	exception 
11	when null_price then 
12	dbms_output.put_line('price is null'); 
13	end; 
14	/ 
Procedure created. 
SQL> exec itsum(101, 500); 
PL/SQL procedure successfully completed. 
SQL> select * from ititems; 
ITEMID ACTUALPRICE ORDID PRODID 
--------- ----------- --------- --------- 
101	2500 500 201 
102	3000 1600 202 
103	4000 600 202 
Procedure For  IN Parameter – Creation, Execution 
SQL> set serveroutput on; 
SQL> create procedure yyy (a IN number) is price number; 
2	begin 
3	select actualprice into price from ititems where itemid=a; 
4	dbms_output.put_line('Actual price is ' || price); 
5	if price is null then 
6	dbms_output.put_line('price is null'); 
7	end if; 
8	end; 
9	/ 
Procedure created. 
SQL> exec yyy(103); 
Actual price is 4000 
PL/SQL procedure successfully completed. 
Procedure For OUT Parameter – Creation, Execution 
SQL> set serveroutput on; 
SQL> create procedure zzz (a in number, b out number) is identity number; 
2	begin 
3	select ordid into identity from ititems where itemid=a; 
4	if identity<1000 then 
5	b:=100; 
6	end if; 
7	end; 
8	/ 
Procedure created. 
SQL> declare 
2	a number; 
3	b number; 
4	begin 
5	zzz(101,b); 
6	dbms_output.put_line('The value of b is '|| b); 
7	end; 
8	/ 
The value of b is 100 
PL/SQL procedure successfully completed. 
Procedure For INOUT Parameter – Creation, Execution 
SQL> create procedure itit ( a in out number) is 
2	begin 
3	a:=a+1; 
4	end; 
5	/ 
 Procedure created. 
SQL> declare 
2	a number:=7; 
3	begin 
4	itit(a); 
5	dbms_output.put_line(„The updated value is „||a); 
6	end; 
7	/ 
The updated value is 8 
PL/SQL procedure successfully completed. 
Tables used: 
SQL>select * from ittrain; 
 TNO TFARE 
 --------- ------------ 
1001	550 
1002	600 
 
Program For Function And It‘s Execution 
SQL> create function trainfn (trainnumber number) return number is 
2	trainfunction ittrain.tfare % type; 
3	begin 
4	select tfare into trainfunction from ittrain where tno=trainnumber; 
5	return(trainfunction); 
6	end; 
7	/ 
Function created. 
SQL> declare 
2	total number; 
3	begin 
4	total:=trainfn (1001); 
5	dbms_output.put_line('Train fare is Rs. '||total); 
6	end; 
7	/ 
Train fare is Rs.550 
PL/SQL procedure successfully completed. 
