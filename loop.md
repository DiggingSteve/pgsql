do $$ \n
declare \n
v_idx integer := 1; \n
v_date TIMESTAMP ; \n
begin \n
  while v_idx < 8000000 loop \n
	v_idx=v_idx+1; \n
	 v_date = get_random_date('2018-01-01','2019-12-31'); \n
    insert into test (id,logdate)values (2,v_date);  -- 执行插入 \n
  end loop;\n
end $$; \n
