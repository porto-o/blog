# XML data type functions

## XML Parse

This function ==converts== a string which has XML values, to a **XML instance**.
```SQL
INSERT INTO employees VALUES (
	'123456',
	'Lopez',
	XMLPARSE(DOCUMENT '<?xml version="1.0"?> <cv
		xmlns="http://www.cv.com/cv"><nombre> ...', WELLFORMED)
);
```
## XML Serialize

Creates a string or LOB containing the contents of an XMLType

```SQL
SELECT e.id, XMLSERIALIZE(DOCUMENT e.cv AS VARCHAR(2000)) AS cv FROM employees e WHERE e.id = 123456;
```
The statement will return de **id** and a **string representation of a resume saved as XMLType** of an specific person.

## XML Element

Creates an XML representation with the values of a relational table.

```SQL
SELECT e.employee_id, XMLELEMENT(NAME "element_name", e.value) AS result FROM HR.employees e;
```

| ID | RESULT |
| --- | ---- |
| 100 | `<element_name>Steven</element_name>` |
| 101 | `<element_name>John</element_name>` |
| 102 | `<element_name>Paul</element_name>` |

```SQL
SELECT XMLELEMENT("Emp", XMLELEMENT("Emp_Name", e.first_name || ' ' || e.last_name),
						 XMLELEMENT("Email", e.email))
AS result FROM HR.employees e;
```

| RESULT |
| --- |
| `<emp><emp_name>ismael</emp_name><email>ismael@gmail.com</email></emp>` |
| `<emp><emp_name>roberto</emp_name><email>roberto@gmail.com</email></emp>` |

```SQL
--OTHER EXAMPLE
```

## XML Attributes

## XML Namespaces

## XML Forest

## XML PI

## XML Comment

## XML Agg

## SYS_XMLGEN


