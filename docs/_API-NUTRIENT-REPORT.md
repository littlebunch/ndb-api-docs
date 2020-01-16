## What is a Nutrient Report?   

A Nutrient Report is a list of foods and their nutrient values for a set of specified nutrients.  This API request provides similar functionality to the Nutrients List component of the NDB search application.  
<br/>

## How it Works

Each nutrient in the NDB is assigned a unique ID (nutrient_id).  You must know this id to retrieve a nutrient report.  A nutrient_id may be obtained by using the list API request.  Please note that nutrient reports are only available for
nutrients in the Standard Release (SR).  Reports are not available for "speciality data" nutrients such as the bioactive compounds nor for foods in the Branded Food Products database.

## Request Parameters 

<p>In addition to the api_key parameter, a request requires at least one nutrient_id in the nutrients parameter.  Up to 20 nutrient_ids may be specified.  Likewise, you may request up to 10 food group id's in the fg parameter.</p>
<table>
<tr class="prop">
<th>Parameter</th><th>Required</th><th>Default</th><th>Description</th>
</tr> 
<tr class="even"><td >api_key</td><td class="value">y</td><td class="value">n/a</td><td class="value">Must be a data.gov registered API key</td>
<tr class="odd"><td>fg</td><td>n</td><td>""</td><td> limit your nutrients to one or more food groups by providing a list of food group ID's via the fg parameter.  The default is a blank list meaning no food group filtering will be applied.  Up to 10 food groups may be specified.</td></tr>
<tr class="even"><td>format<sup>1</sup></td><td>n</td><td>JSON</td><td>Report format: xml or json</td></tr>
<tr class="odd"><td>max</td><td>n</td><td>50</td><td>Number of rows to return.  The maximum per request is 1,500.</td></tr>
<tr class="even"><td>offset</td><td>n</td><td>0</td><td>beginning row in the result set to begin </td></tr>
<tr  class="even"><td>nbno</td><td>n</td><td>n/a</td><td>Report the nutrients for a single food identified by it's unique id -- nutrient number</td></tr>
<tr  class="odd"><td>nutrients</td><td>y</td><td>n/a</td><td>a list of up to a maximum of 20 nutrient_id's to include in the report</td></tr>
<tr  class="even"><td>sort</td><td>n</td><td>f</td><td>Sort the list of foods by (f)ood name or nutrient (c)ontent.  If you are requesting more than one nutrient and specifying sort = c then the first nutrient in your list is used for the content sort.</td></tr>
<tr  class="odd"><td>subset</td><td>n</td><td>0</td><td>You may indicate all the foods in the SR database or an abridged list from the pull down menu. Set the subset parameter to 1 for the abridged list of about 1,000 foods commonly consumed in the U.S. The default 0 for all of the foods in the database </td></tr>

</table>
<sup>1</sup>Format can also be sent in the request header:  Content-Type: application/json or Content-Type:application/xml. 

## Response Elements 

<p>A response is structured as a list of one or more foods.  Each food has list of one or more nutrients. </p>
 
<table>
<tr>
<th style="font-style:italic">report</th><th colspan="2">basic information about the report</th></tr>  
</tr>
<tr><td></td><td style="font-style:italic">group</td><td>If applicable, the list of food groups used to filter the report </td></tr> 
<tr class="odd"><td></td><td style="font-style:italic">subset</td><td>The name of the subset of foods in the response or all foods </td></tr>  

<tr class="even"><td></td><td style="font-style:italic">sr</td><td>Standard Release version of the data being reported</td></tr>  
<tr class="odd"><td></td><td style="font-style:italic">end</td><td>The number of the last item in the reports -- normally start + max.</td></tr> 
<tr><td></td><td style="font-style:italic">start</td><td>Value of the offset parameter used in the report</td></tr>  
<tr class="odd"><td></td><td style="font-style:italic">total</td><td>The total number of items available in the reports.  Useful for paging the report.</td></tr>  

<tr>
<th style="font-style:italic">foods</th><th colspan="2">A list of foods</th></tr>  
<tr class="odd"><td></td><td style="font-style:italic">ndbno</td><td>  NDB food number </td></tr>  
<tr><td></td><td style="font-style:italic">name</td><td> food name </td></tr> 
 <tr  class="odd"><td></td><td style="font-style:italic">measure </td><td>The household measure represented by the nutrient value element</td></tr>
<tr><td></td><td style="font-style:italic">nutrients</td><td>The list of nutrients and their values for a food</td></tr>
<tr  class="odd"><td></td><td style="font-style:italic">nutrient_id</td><td>Nutrient Number</td></tr>
 <tr><td></td><td style="font-style:italic">nutrient</td><td>Description of the nutrient</td></tr>   
 <tr class="odd"><td></td><td style="font-style:italic">unit</td><td>Unit in which the nutrient value is expressed</td></tr>
   <tr><td></td><td style="font-style:italic">gm</td><td>The 100 gram equivalent value for the nutrient</td></tr>  
  <tr class="odd"><td></td><td style="font-style:italic">value</td><td>Value of the nutrient for this food</td></tr>   
 

 </table> 
 
## Some Examples 

<p>Here's some nutrient reports you can obtain for Total lipids (nutrient_id=204, ), calories (nutrient_id=208), carbohydrates (nutrient_id=205) and sugars (nutrient_id=269) in either XML or JSON.</p>

#### XML 

All foods:   
 Browser:  https://api.nal.usda.gov/ndb/reports/?nutrients=204&nutrients=208&nutrients=205&nutrients=269&max=50&offset=25&format=xml&api_key=DEMO_KEY 
CURL:  curl -H "Content-Type:application/xml" -d '&lt;report&gt;&lt;fg&gt;0100&lt;/fg&gt;&lt;fg&gt;0500&lt;/fg&gt;&lt;nutrients&gt;204&lt;/nutrients&gt;&lt;nutrients&gt;208&lt;/nutrients&gt;&lt;nutrients&gt;205&lt;/nutrients&gt;&lt;nutrients&gt;269&lt;/nutrients&gt;&lt;max&gt;50&lt;/max&lt;offset&gt;25&lt;/offset&gt;&lt;/report&gt;' DEMO_KEY@api.nal.usda.gov/ndb/nutrients  
  <p>
For food groups Dairy and Egg Products (id = 0100) and Poultry Products ( id=0500)    
Browser:  https://api.nal.usda.gov/ndb/reports/?fg=0100&fg=0500&nutrients=204&nutrients=208&nutrients=205&nutrients=269&max=50&offset=25&format=xml&api_key=DEMO_KEY
 <br/>
CURL:  curl -H "Content-Type:application/xml" -d '&lt;report&gt;&lt;fg&gt;0100&lt;/fg&gt;&lt;fg&gt;0500&lt;/fg&gt;&lt;nutrients&gt;204&lt;/nutrients&gt;&lt;nutrients&gt;208&lt;/nutrients&gt;&lt;nutrients&gt;205&lt;/nutrients&gt;&lt;nutrients&gt;269&lt;/nutrients&gt;&lt;max&gt;50&lt;/max&gt;&lt;offset&gt;25&lt;/offset&gt;&lt;/report&gt;' DEMO_KEY@api.nal.usda.gov/ndb/nutrients
</p>
<p>
For chedder cheese (ndbno 01009) only:  
Browser: http://api.nal.usda.gov/ndb/reports/?nutrients=204&nutrients=208&nutrients=205&nutrients=269&ndbno=01009&max=50&offset=25&format=xml&api_key=DEMO_KEY
 <br/>
CURL:  curl -H "Content-Type:application/xml" -d '&lt;report&gt;&lt;ndbno&gt;01009&lt;/ndbno&gt;&lt;nutrients&gt;204&lt;/nutrients&gt;&lt;nutrients&gt;208&lt;/nutrients&gt;&lt;nutrients&gt;205&lt;/nutrients&gt;&lt;nutrients&gt;269&lt;/nutrients&gt;&lt;max&gt;50&lt;/max&gt;&lt;offset&gt;25&lt;/offset&gt;&lt;/report&gt;' DEMO_KEY@api.nal.usda.gov/ndb/nutrients    
</p>

#### JSON  

All foods:     
Browser: https://api.nal.usda.gov/ndb/nutrients/?format=json&api_key=DEMO_KEY&nutrients=205&nutrients=204&nutrients=208&nutrients=269 
CURL:  curl -H "Content-Type:application/json" -d '{"nutrients":["204","205","208","269"],"max":25,"offset":0}' DEMO_KEY@api.nal.usda.gov/ndb/nutrients  
 <p>
For food groups Dairy and Egg Products (id = 0100) and Poultry Products (id=0500):   
Browser: https://api.nal.usda.gov/ndb/nutrients/?format=json&api_key=DEMO_KEY&nutrients=205&nutrients=204&nutrients=208&nutrients=269&fg=0100&fg=0500
 <br/>
CURL:  curl -H "Content-Type:application/json" -d '{"nutrients":["204","205","208","269"],"fg":["0100","0500"],"max":25,"offset":0}' DEMO_KEY@api.nal.usda.gov/ndb/nutrients  
</p>
<p>
For chedder cheese (ndbno 01009) only:   
Browser: https://api.nal.usda.gov/ndb/nutrients/?format=json&api_key=DEMO_KEY&nutrients=205&nutrients=204&nutrients=208&nutrients=269&ndbno=01009
 <br/>
CURL:  curl -H "Content-Type:application/json" -d '{"nutrients":["204","205","208","269"],"ndbno":"01009","max":25,"offset":0}' DEMO_KEY@api.nal.usda.gov/ndb/nutrients  
</p>
