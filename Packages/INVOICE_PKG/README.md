The purpose of this package is to scan the table for customers who have not yet received their invoce, if they have not, then they 
will receive an email with relevant purchase information, it also contains several useful testing subprograms for the developer.

==========================================================Running Requirements==========================================================

--CREATES THE TABLE NEEDED TO RUN THE SUBPROGRAMS IN THE INVOICE_PKG PACKAGE

create table email_log (
    order_id number primary key,
    first_name varchar2(55) not null,
    last_name varchar2(55) not null,
    address varchar2(155) not null,
    phone_number number not null,
    email varchar2(75) not null,
    status varchar2(15) not nul,
    confirmation_number varchar2(10)
);

--POPULATES THE TABLE 

BEGIN
    insert into email_log values (1, 'Mike', 'Mike', '123 old street drive', 0001112222, 'mike@xmail.com', 'PENDING');
    insert into email_log values (2, 'Stan', 'Stan', '456 old street drive', 0002224444, 'stan@xmail.com', 'PENDING');
    insert into email_log values (3, 'Tim', 'Tim', '789 old street drive', 0003335555, 'tim@xmail.com', 'PENDING');
END;

--QUICK TEST TO MAKE SURE OUR TABLE POPULATED CORRECTLY
select * from email_log;

--STATEMENT NEEDED TO RUN PACKAGE
execute invoice_pkg.scan_for_emails;

--Creates unique confirmation numbers for every customer
exec invoice_pkg.populate_with_conf_num;

