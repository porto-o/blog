# Introduction

The function `XMLTable()` and `XMLQuery()` are part of the SQL/XML standard and they are something like **an interface between SQL and XQuery**.

# XML Table function

The function `XMLTable()` is used to divide the result of an XQuery statement, and put all the pieces in a virtual table.

### Example

```SQL
SELECT l.lineitem, l.description, l.partId, l.unitprice, l.quantity FROM purchaseOrder,
	XMLTable('for $i in /PurchaseOrder/LineItems/LineItem where $i/@ItemNumber >= 8 and $i/Part/@UnitPrice > 50 and $i/Part/@Quantity > 2 return $i' PASSING OBJECT_VALUE
COLUMNS 
lineitem NUMBER PATH '@ItemNumber',
description VARCHAR (30) PATH 'Description',
partid NUMBER PATH 'Part/@Id',
unitprice NUMBER PATH 'Part/@UnitPrice',
quantity NUMBER PATH 'Part/@Quantity') 1;
```

