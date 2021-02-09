# Complex Iteration Flows
### Overview

When the originating Actor's output is a complex object, the iteration's complexity increases due to the object's internal hierarchy of fields and nested arrays. Thus the iteration logic over an object with multiple links is impacted by the answers to the following questions:

* Are the connected elements on the same level of hierarchy or on different levels?
* Are the link types the same (all **Iterate**) or different (**Iterate** combined with other types)?
* Do the connected elements belong to different nested arrays, and if yes - do they have the same or different size? 

This article described how Broadway performs complex iteration use cases, such as:

* Loop over multiple elements of a complex object on different levels of the object's hierarchy, for example a field and a nested array.
* Use different connection line types when iterating over a complex object's elements.
* Iterate over multiple arrays in the same iteration.

If the connected elements of the object are on the same level of hierarchy (such as two fields of the same array), the iteration behavior is the same as the iteration over [two or more elements in a result array](21_iterations.md#iterate-over-two-or-more-elements) as described in the previous article. 

### Iterate Over Both an Element and a Nested Array

* The connected elements are on different levels of hierarchy: **entityType** field in [resources] array and **objectType** field in [hardware] nested array.
* Both are connected using the **Iterate** link type. 
* The iteration runs over all **entityTypes** of the [resources] array, and for each one - over all the elements of the [hardware] nested array.

<img src="images/iterate_mult_02.PNG" alt="image" style="zoom:80%;" />

### Iterate Over a Field and Take a Nested Array by Value

- The connected elements are on different levels of hierarchy: **entityType** field in [resources] array and the **[hardware]** nested array.
- The **entityType** is connected using the **Iterate** link type, while the **[hardware]** nested array is connected using the **Value** link type.
- The iteration runs over all **entityTypes** of the [resources] array, and for each **entityType** takes all its hardware (the nested array's data).

<img src="images/iterate_mult_03.PNG" alt="image" style="zoom:80%;" />

### Iterate Over a Field and Take a First Value of a Nested Array

* This is a private case of the previous scenario with the same connected elements.
* The **entityType** is connected using the **Iterate** link type, while the **[hardware]** nested array is connected using the **First** link type.
* The iteration runs over all **entityTypes** of the [resources] array, and for each **entityType** takes the first element of its hardware nested array.

<img src="images/iterate_mult_05.PNG" alt="image" style="zoom:80%;" />

### Take an Array by Value and Iterate Over a Field in the Same Array

* The connected elements are on different levels of hierarchy: **entityType** field in [resources] array and the whole **[resources]** array.
* The **entityType** is connected using the **Iterate** link type, while the **[resources]** array is connected using the **Value** link type.
* The iteration runs over all **entityTypes** of the [resources] array while during each iteration - the whole [resources] array is passed by value (the same data in all iterations).

<img src="images/iterate_mult_04.PNG" alt="image" style="zoom:80%;" />

### Iterate Over Multiple Arrays

The originating Actor's output can have more than one collection. A common use case is a JSON data structure that contains more than one array.
Occasionally it may be required to manage several loops over the same data structure, for example in order to combine the data from two arrays or to perform other kind of data manipulation. In this case, both arrays (or elements in the arrays) need to be connected using an **Iterate** link type to one or more Actors. 

In this case the iteration logic is impacted by the answers to the question - do these arrays have the same or different size? When the arrays have different size, at some point one of them is finished and returns a null while the another one still has values. To prevent the redundant loops over the empty array, use the **IsNull** Actor to check if the array returns a value or null.

![image](images/iterate_blend1.PNG)

Another recommended way to handle two collections with different sizes is by using the [Inner Flows](22_broadway_flow_inner_flows.md). You can pass each array by value into its respective inner flow and then iterate inside each inner flow on the array values.

![image](images/iterate_blend2.PNG)



[![Previous](/articles/images/Previous.png)](21_iterations.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](22_broadway_flow_inner_flows.md)

