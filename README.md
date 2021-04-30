```
Create table Transaction(
    itemno INTEGER,
    itemname varchar(25),
    rate INTEGER,
    qty INTEGER,
    total INTEGER
);
Create or replace trigger enter_total
Before Insert on Transaction
for each row
BEGIN
    :NEW.total := :NEW.rate * :NEW.qty;
END;
/
insert INTO Transaction values( 1 ,' soap ', 12 , 2 , 0);
insert INTO Transaction values( 2 ,' biscuit ', 25 , 4 , 0);
insert INTO Transaction values( 3 ,' honey ', 30 , 3 , 0);
insert INTO Transaction values( 4 ,' matchstick ', 5 , 6 , 0);
insert INTO Transaction values( 5 ,' chips ', 17 , 5 , 0);
insert INTO Transaction values( 6 ,' cold drinks ', 20 , 1 ,0 );
insert INTO Transaction values( 7 ,' sev ', 5 , 7 , 0);
```


```
Create table Item_Master(
    Itemid INTEGER PRIMARY KEY,
    Description varchar(100),
    Bal_Stock INTEGER
);

Create table Item_Transaction(
    Itemid INTEGER PRIMARY KEY,
    Description varchar(100),
    Quantity INTEGER
);
```

