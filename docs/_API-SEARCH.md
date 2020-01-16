## What are Searches?   

<p>A search request sends keyword queries and returns lists of foods which contain one or more of the keywords in the food description, scientific name, or commerical name fields.  Search requests are a good way to locate NDB numbers (NDBno) for the <g:link controller="doc" action="apilist" id="API-FOOD-REPORT.md">reports</g:link> API as well as for general discovery.</p> 

## How it Works  

<p>There are no restrictions, other than common sense, on the keywords which can be searched.  It's very easy to create paged browsing by using the total and offset (a zero-based start point) parameters.  You may want to try the <g:link controller="foods" action="list">discovery application</g:link> to get a feel for how searching works.  You may limit your search results to a specific food group by specifying a food group id or a food group description in the <i>fg</i> parameter.  (You may wish to use the <g:link controller="doc" action="apilist" id="API-LIST.md">list</g:link> request to identify the food group id or description you wish to use.)   </p>

## Parameters

<p>The only required parameter for a valid search request is your authentication key (api_key).  The default sort order of results list is "relevance", i.e. how closely a food matches the query terms.</p>  
<table>
<tr><th> Name</th><th>Required</th><th>Default</th><th>Description</th></tr>   
<tr><td>api_key</td><td>y</td><td>n/a</td><td>Must be a data.gov registered API key</td></tr>   
<tr class="odd"><td>q</td><td>n</td><td>""</td><td>Search terms</td></tr>
<tr><td>ds</td><td>n</td><td>""</td><td>Data source.  Must be either 'Branded Food Products' or 'Standard Reference'</td></tr>
<tr class="odd"><td>fg</td><td>n</td><td>""</td><td>Food group ID</td></tr>
<tr><td>sort</td><td>n</td><td>r</td><td>Sort the results by food name (n) or by search relevance (r)</td></tr>
<tr class="odd"><td>max</td><td>n</td><td>50</td><td>maximum rows to return</td></tr>
<tr><td>offset</td><td>n</td><td>0</td><td>beginning row in the result set to begin </td></tr>
<tr class="odd"><td>format<sup>1</sup></td><td>n</td><td>JSON </td><td>results format: json or xml</td></tr>
</table>
<sup>1</sup>Format can also be sent in the request header:  Content-Type: application/json or Content-Type:application/xml.           

## Response Elements

<p>A search response consists of information about the results of the search such as the total hits matching the query and the starting and ending points in the results list, followed by a list of foods.  Metadata for each food in the returned list includes the food's description (name) and NDBno.</p>
<p>
<table>
<tr><th>list</th><th colspan="2">information about the items returned</th></tr>       
<tr><td></td><td style="font-style:italic">q</td><td>terms requested and used in the search</td></tr>   
<tr class="odd"><td></td><td style="font-style:italic">       start</td><td>beginning item in the list</td></tr>     
<tr><td></td><td style="font-style:italic">       end</td><td>last item in the list</td></tr>       
<tr class="odd"><td></td><td style="font-style:italic">       offset</td><td>beginning offset into the results list for the items in the list requested</td></tr>      
<tr><td></td><td style="font-style:italic">total</td><td>total # of items returned by the search</td></tr>    
<tr class="odd"><td></td><td style="font-style:italic">sort</td><td>requested sort order (r=relevance or n=name) </td></tr>    
<tr><td></td><td style="font-style:italic">fg</td><td>food group filter </td></tr> 
<tr class="odd"><td></td><td style="font-style:italic">sr</td><td>Standard Release version of the data being reported</td></tr>   
 <tr class="odd"><th>item</th><th  colspan="2">individual items on the list </th></tr>  
 <tr><td></td><td style="font-style:italic">ndbno </td><td> the food’s NDB Number</td></tr>    
 <tr class="odd"><td></td><td style="font-style:italic">name</td><td> the food’s name </td></tr>   
 <tr><td></td><td style="font-style:italic">group</td><td> food group to which the food belongs </td></tr> 
 <tr class="odd"><td></td><td style="font-style:italic">ds</td><td> Data source:  BL=Branded Food Products or SR=Standard Release</td></tr> 
<tr><td></td><td style="font-style:italic">manu</td><td>The foods manufacturer</td></tr> 

</table>
</p>

### Examples

<p>The examples below show how you might request a search for foods containing the word "butter" limiting the results to only those foods in the "Dairy and Egg Products" food group.</p>

#### XML   

<nobrk><b>Browser</b>: https://api.nal.usda.gov/ndb/search/?format=xml&q=butter&max=25&offset=0&api_key=DEMO_KEY </nobrk>     
<nobrk><b>Curl</b>: curl -H "Content-Type: application/xml" -d '&lt;list&gt;&lt;q&gt;butter&lt;/q&gt;&lt;max&gt;25&lt;/max&gt;&lt;offset&gt;0&lt;/offset&gt;&lt;/list&gt;' DEMO_KEY@api.nal.usda.gov/ndb/search</nobrk>   

#### JSON

<b>Browser</b>: https://api.nal.usda.gov/ndb/search/?format=json&q=butter&sort=n&max=25&offset=0&api_key=DEMO_KEY
<b>Curl</b>: curl -H "Content-Type: application/json" -d '{"q":"butter","max":"25","offset":"0"}' DEMO_KEY@api.nal.usda.gov/ndb/search    
