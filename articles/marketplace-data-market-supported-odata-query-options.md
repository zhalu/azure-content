 
<properties 
   pageTitle="Supported OData Query Options" 
   description="What are Supported OData Query Options" 
   services="cloud-services" 
   documentationCenter="" 
   authors="kevinscharpenberg" 
   manager="manager-alias" 
   editor=""/>

<tags
   ms.service="marketplace"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="data-services" 
   ms.date="02/13/2015"
   ms.author="kevsch"/>
#Supported OData Query Options 

 -----------
When you develop an application that uses the Windows Azure Marketplace (WAM) there are some considerations and limitations you need to be aware of. 

 
 -----------
###In This Topic

<table>
  <tr>
<td>Supported OData Query Options
</td><td>OData operations and functions that are supported by the Marketplace. For example: $orderby.
</td>
</tr>

<td> Determine DataServiceVersion
 </td>
<td>How to determine the DataServiceVersion.
</td>
</tr>
</table>

All data feeds from the Marketplace are OData feeds. Read about OData at the [OData](http://www.odata.org/) site. The Marketplace provides limited support for OData queries. The following list identifies the supported functionality for Services and OData.

###Supported OData Query Options

<table>
<tr>
<td>$top
</td>
<td>The maximum number of items returned in the result set for each page.
</td>
</tr>
<td>$skip
</td>
<td>The number of rows to skip in the result set before beginning to return results.

</td>
</tr><td>$filter
</td>
<td>

*  Comparisons <br>
Eq – Equal to <br>
Gt – Greater than <br> 
Lt – Less than <br>
Ne – Not equal to <br>

<br>
*  Concatinations <br>
And <br>
Or

<br><br>
*  Field Names - Types: all OData supported types.
</td>




</tr><td>$orderby
</td>
<td>Specifies the sort order of the result set. <br>
NOTE: Requires DataServiceVersion 2.0 or higher. To determine DataServiceVersion see Determine DataServiceVersion later in this topic.

</td>
</tr><td>$select
</td>
<td> Specifies the fields returned in the result set.

</td>
</tr><td>$skiptoken
</td>
<td>An opaque value that must be passed back to the server in order to continue getting results for the query. <br> For more information see Skip Token System Query Option ($skiptoken) at OData.org.

</td>
</tr><td>$count
</td>
<td>Returns the count of a collection of entities. <br>
NOTE: Requires DataServiceVersion 2.0 or higher. To determine DataServiceVersion see Determine DataServiceVersion in this topic.

</td>
</tr><td>$inlinecount
</td>
<td>$inlinecount is only supported for flexible query services. It is not supported for fixed query services. <br>
NOTE: Requires DataServiceVersion 2.0 or higher. To determine DataServiceVersion see Determine DataServiceVersion later in this topic.

</td>
</tr><td>$metadata
</td>
<td>Retrieves a list of fields, their data types, mode, and other related information in a dataset.

</td>
</tr><td>ID operators

</td>
<td>E.g. "/Companies('Microsoft')"

</td>
</tr><td>Comparison operators

</td>
<td>eq – Equal to <br>
ne – Not equal to <br>
lt – Less than <br>
le – Less than or equal to <br>
gt – Greater than <br>
ge – Greater than or equal to <br>

</td>
</tr>


</td>
</tr><td>Logical operators
</td>
<td>and – True only if both operands are true <br>
or – True if either or both operands are true <br>
not – opposite of operand 


</tr><td>Arithimetic operators


</td>
<td>add – Addition operator <br>
sub – Subtraction operator<br>
mult – Multiplication operator<br>
div – Division operator<br>
mod – Modulo (remainder after integer division) operator

</tr><td>Grouping operators
</td>
<td>( and )

</tr><td>DateTime Functions

</td>
<td>year<br>
month<br>
day<br>
hour<br>
minute<br>
second


</tr><td>Math functions

</td>
<td>round<br>
ceiling<br>
floor
</td>
</tr>
</table>


###Determine DataServiceVersion
To detect the DataServiceVersion:

1. Make your request
2. Look at the HTTP header: DataServiceVersion

##See Also
###Other Resources
OData Home Page <br>
OData URI conventions
