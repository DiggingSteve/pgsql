<h1>使用触发器自动生成表 但是在11版本下 并不能创建全局主键</h1>
create table tbl_inherits_test
(
    a int ,
    b timestamp without time zone
);
create index idx_tbl_inherits_test_b on tbl_inherits_test using btree (b);


create or replace function f_insert_tbl_inherits_test() returns trigger as
$body$
declare tablename varchar(32) default '';
begin
    tablename='tbl_inherits_test_'||to_char(NEW.b,'YYYY_MM_DD');
   
    execute 'insert into '||tablename||'(a,b) values('||NEW.a||','''||NEW.b||''')';
    return null;
    EXCEPTION
        when undefined_table then
        execute 'create table '||tablename||'() inherits (tbl_inherits_test)';
        execute 'create index idx_'||tablename||'_b on '||tablename||' using btree(b)';
        execute 'insert into '||tablename||'(a,b) values('||NEW.a||','''||NEW.b||''')';
    return null;    
end;
$body$
language plpgsql;

create trigger trg_insert_tbl_inherits_test before insert on tbl_inherits_test for each row execute procedure f_insert_tbl_inherits_test();

alter table tbl_inherits_test add PRIMARY key (a)

insert into tbl_inherits_test(a,b) values(1,'2013-06-20 17:40:21');
