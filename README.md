# End Sems Lab
### Date: 30-04-2021

## Question 1

### Create Table 
``` 
Create table Containers(
    color varchar(20),
    parent_color varchar(20),
    count INTEGER Default 1,
    PRIMARY KEY(color, parent_color)
);
```

### Procedure
```
Create or Replace procedure insert_color(co IN varchar, pco IN varchar) 
IS
cal NUMBER;
BEGIN   
    Select count(*) into cal from Containers where color = co and parent_color = pco;
    if(cal > 0) then
        Update Containers set count = count + 1 where color = co and parent_color = pco;
    else
        Insert into Containers values(co, pco, 1);
    end if;
END;
/
```

### Insert Statements
```
BEGIN
    insert_color( ' blue ',' NULL ' );
    insert_color( ' red ',' blue ' );
    insert_color( ' green ',' blue ' );
    insert_color( ' blue ',' red ' );
    insert_color( ' green ',' red ' );
    insert_color( ' red ',' green ' );
    insert_color( ' blue ',' green ' );
    insert_color( ' white ',' blue ' );
    insert_color( ' white ',' blue ' );
    insert_color( ' green ',' white ' );
    insert_color( ' yellow ',' white ' );
    insert_color( ' purple ',' green ' );
    insert_color( ' yellow ',' green ' );
    insert_color( ' blue ',' purple ' );
    insert_color( ' green ',' yellow ' );
    insert_color( ' white ',' red ' );
    insert_color( ' white ',' red ' );
    insert_color( ' yellow ',' white ' );
    insert_color( ' blue ',' white ' );
    insert_color( ' yellow ',' blue ' );
    insert_color( ' white ',' blue ' );
    insert_color( ' purple ',' yellow ' );
    insert_color( ' red ',' white ' );
END;
/
```

```
Create table color_code(
    id INTEGER,
    color varchar(25),
    total_inside INTEGER
);
insert INTO color_code values( 1 ,' Blue ', 22 );
insert INTO color_code values( 2 ,' Red ', 10 );
insert INTO color_code values( 3 ,' Blue ', 4 );
insert INTO color_code values( 4 ,' White ', 1 );
insert INTO color_code values( 5 ,' White ', 1 );
insert INTO color_code values( 6 ,' Green ', 0 );
insert INTO color_code values( 7 ,' Yellow ', 0 );
insert INTO color_code values( 8 ,' Green ', 4 );
insert INTO color_code values( 9 ,' Purple ', 2 );
insert INTO color_code values( 10 ,' Yellow ', 2 );
insert INTO color_code values( 11 ,' Blue ', 0 );
insert INTO color_code values( 12 ,' Green ', 0 );
insert INTO color_code values( 13 ,' Green ', 10 );
insert INTO color_code values( 14 ,' Red ', 4 );
insert INTO color_code values( 15 ,' White ', 1 );
insert INTO color_code values( 16 ,' White ', 1 );
insert INTO color_code values( 17 ,' Yellow ', 0 );
insert INTO color_code values( 18 ,' Blue ', 0 );
insert INTO color_code values( 19 ,' Blue ', 4 );
insert INTO color_code values( 20 ,' Yellow ', 1 );
insert INTO color_code values( 21 ,' White ', 1 );
insert INTO color_code values( 22 ,' Purple ', 0 );
insert INTO color_code values( 23 ,' Red ', 0 );
```

### Output
```
Select * from Containers;
```

## Queries
### 1
```
Select sum(count) from Containers;
```

### 2
```
DECLARE
    mcount color_code.total_inside%type;
BEGIN
    Select max(total_inside) into mcount from color_code;
    
    FOR items in (Select * from color_code where total_inside = 22)
    LOOP
        dbms_output.put_line('Max Size Circle is ' ||  items.id || ' of color ' || items.color);
    end loop;
    
    Select min(total_inside) into mcount from color_code;
    FOR items in (Select id, color from color_code where total_inside = 0)
    LOOP
        dbms_output.put_line('Min Size Circle is ' ||  items.id || ' of color ' || items.color);
    end loop;

END;
/
```

### 3
```
Select color, max(total_inside), min(total_inside)
from color_code
group by color;
```

### 4
```
Select sum(total_inside) from color_code where color = 'Blue';
```

### 5
```
Select sum(total_inside) from color_code where color = 'Green';
```

### 6
```
Select count(*) from color_code where color = 'White';
```

### 7
```
Select count(*) from color_code where color = 'Yellow';
```

### 8
```
Select count(*) from color_code where color in ('Red', 'Purple);
```
### 9
```
Select color from color_code where total_inside NOT IN (Select max(total_inside) from color_code where total_inside NOT IN(Select max(total_inside) from color_code where total_inside NOT IN (Select max(total_inside) from color_code)));
```


### 10
```
Select id from color_code where total_inside >= 4;
```




