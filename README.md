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

### Output
```
Select * from Containers;
```



