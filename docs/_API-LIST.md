## What are Lists?
<p>You may request a list of foods, nutrients or food groups.  List requests are good for providing your users with a paged browse and select experience.  For example, your application might allow users to select a food from a foods list to generate a <g:link controller="doc" action="apilist" id="API-FOOD-REPORT.md">Food Reports</g:link> request.</p>   

## How it Works
<p>Basically, you need to indicate the type of list you're requesting and the number of items you want returned on the list up to a maximum of 1500 items in a single request.  You can also specify an offset (a zero-based start point) into a list for a paged experience.</p>

## Request Parameters  
<p>Your api_key is the only required parameter to generate a list.  With no other parameters the request will return 50 foods items sorted by food name beginning with the first item (0 offset) in JSON format.</p>  
<table>
<tr><th>Name</th><th>Required</th><th>Default</th><th>Description</th></tr>
<tr><td>api_key</td><td>y</td><td>n/a</td><td>Must be a data.gov registered API key</td></tr> 
<tr class="odd"><td>lt</td><td>n</td><td>f</td><td>list type(lt): d = derivation codes, f = food , n = all nutrients, ns = speciality nutrients, nr = standard release nutrients only,g = food group</td></tr>  
<tr><td>max</td><td>n</td><td>50</td><td> maximum number of items to return</td></tr> 
<tr class="odd"><td >offset</td><td>n</td><td>0</td><td> beginning item in the result set</td></tr>  
<tr><td>sort</td><td>n</td><td>n</td><td> sort order:  n=name or id (Meaning of id varies by list type: nutrient number for a nutrient list, NDBno for a foods list ,food group id for a food group list</td></tr>  
<tr class="odd"><td>format<sup>1</sup></td><td>n</td><td>JSON</td><td>report format: JSON or XML</td></tr>
</table>   

<sup>1</sup>Format can also be sent in the request header:  Content-Type: application/json or Content-Type:application/xml.      
## Response Elements  
<p>The list response is very simple, consisting of some metadata about your request and a list of names and id's.  The meaning of the name and id elements are dependent on the type of list requested in the <i>lt</i> parameter.  If you have
requested a list of foods, then the name element will refer to the name of the food and the id to the food's NDBno.  For food groups lists, name references the name of the food group and id to the food group's unique id.  And, for nutrients, name refers to the nutrient name and id to the unique id assigned to each nutrient in the database called nutrient_no.</p>
<p><table>
<tr><th> list </th><th colspan="2"> information about the request and the items returned </th></tr>  
<tr><td></td><td style="font-style:italic"> type </td><td> type of list requested </td></tr>  
<tr class="odd"><td></td><td style="font-style:italic"> start </td><td> beginning offset </td></tr>  
<tr><td></td><td style="font-style:italic"> end</td><td> ending offset </td></tr>  
<tr class="odd"><td></td><td style="font-style:italic"> total </td><td>number of items in the list </td></tr>    
<tr><td></td><td style="font-style:italic"> sort </td><td> sort order of the list</td></tr> 
<tr class="odd"><td></td><td style="font-style:italic">sr</td><td>Standard Release version of the data being reported</td></tr>   
  <tr class="odd"><th> item </th><th colspan="2"> information about individual items on the list </th></tr>  
<tr><td></td><td style="font-style:italic"> id</td><td>ndbno for type 'f'; nutrient no for type 'n' or group no for type 'g' </td></tr>  
<tr class="odd"><td></td><td style="font-style:italic">name</td><td>item name </td></tr>
</table>
</p>

## Some Examples 
<p>These examples illustrate how to request a list of foods sorted by food name.</p>  

### XML:  
<b>Browser</b>: <a href="${grailsApplication.config.gov.usda.nal.ndl.api.URL}/list?format=xml&lt=f&sort=n&api_key=DEMO_KEY" title="Link to sample API request" >https://api.nal.usda.gov/ndb/list?format=xml&lt=g&sort=n&api_key=DEMO_KEY</a>     
<b>CURL</b>: curl -H "Content-Type:application/xml" -d '&lt;list&gt;&lt;lt&gt;f&lt;/lt&gt;&lt;sort&gt;n&lt;/sort&gt;&lt;/list&gt;' DEMO_KEY@api.nal.usda.gov/ndb/list

### JSON:  
<b>Browser</b>: <a href="${grailsApplication.config.gov.usda.nal.ndl.api.URL}/list?format=json&lt=f&sort=n&api_key=DEMO_KEY" title="Link to sample API request" >https://api.nal.usda.gov/ndb/list?format=json&lt=f&sort=n&api_key=DEMO_KEY</a>   
<b>CURL</b>: curl -H "Content-Type:application/json" -d '{"lt":"f","sort":"n"}' DEMO_KEY@api.nal.usda.gov/ndb/list   

