# Extract

Returns the selected node and its children nodes, up to the leafs.

```SQL
SELECT EXTRACT(table_name, '/element').getstringval() AS return FROM 
```

### Example

Let's take a look at the following example. We have the same `employees`table, however the XML document that we will be working with looks like this:

```XML
<employee>
	<name> Ismael Porto García </name>
	<phone> 123456 </phone>
	<languages> Python, Java, C, JavaScript </languages>
	<projects>
		<project>
			<name> Bad Bank </name>
			<description> Just a description of the Bad Bank project </description>
		</project>
		<project>
			<name> E-Market </name>
			<description> Just a description of the E-Market project </description>
		</project>
	</projects>
</employee>
```

After inserting this XML to our table on the column `resume`, we will use the **extract function** to get the list of projects.

```SQL
SELECT EXTRACT(resume, '/employee/projects').getstringval() AS output FROM employees;
```

![[Pasted image 20231023141644.png]]


# Exists Node

Return True if there is a leaf with an specific value.

```SQL
SELECT count(*) FROM table_name WHERE existsNode(column_name,'/path[element=value]' = 1)
```
### Example

Let's take again the XML from the previous function, but now we want to know **if there is an element `name` inside `projects` tree where the value is ` Bad Bank `

```SQL
SELECT count(*) FROM employees
WHERE existsNode(resume, '/employee/projects/project[name=" Bad Bank "]') = 1;
```

![[Pasted image 20231023142854.png]]

# Extract value

This function returns ==the value== of a leaf node, therefore we **must take care of not returning an XML**.

```SQL
SELECT extractValue(column_name, '/path_to_leaf') AS output FROM table_name;
```
### Example

Let's extract the value of the `name element`from the same XML document.

```SQL
SELECT extractValue(resume, '/employee/name') AS output FROM employees;
```

![[Pasted image 20231023143305.png]]

>[!Warning] You must take care of declaring an XPath to a leaf not to a tree of nodes

---
Next topic ➡️ [[XMLTable and XMLQuery]]

