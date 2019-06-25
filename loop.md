do $$
declare
v_idx integer := 1;
v_date TIMESTAMP ;
begin
  while v_idx < 8000000 loop
	v_idx=v_idx+1;
	 v_date = get_random_date('2018-01-01','2019-12-31');
    insert into test (id,logdate)values (2,v_date);  -- 执行插入
  end loop;
end $$;
