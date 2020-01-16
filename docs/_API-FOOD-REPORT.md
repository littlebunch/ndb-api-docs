## What is a Food Report Version 1?   

A Food Report is a list of nutrients and their values in various portions for a specific food. 
<br/>
Reports are available in three formats: basic, full or statistics.  A “Basic Report” contains a limited set of nutrients, based upon those found on a nutrition facts panel of a package of food, or frequently requested while a “Full Report” contains all the nutrients found in SR for that food. The "Statistics Report" provides all the statistical parameters available in SR. 
<br/>
<br/>
Please note that reports for foods from the Branded Food Products database are only availalbe in a "basic" format.  So, even though you may request a "Full" or "Statistics" report for Branded Food Products foods, you will only receive a "Basic" report.

## How it Works

Each food in the NDB is assigned a unique ID called the NDB number (NDBno).  You must know a food's NDBno to retrieve a report.  If you don't know a food's NDBno you may use either the list or search API to obtain it.   

## Request Parameters  

<table>
<tr class="prop">
<th>Parameter</th><th>Required</th><th>Default</th><th>Description</th>
</tr> 
<tr class="even"><td >api_key</td><td class="value">y</td><td class="value">n/a</td><td class="value">Must be a data.gov registered API key</td>
<tr  class="odd"><td>ndbno</td><td>y</td><td>n/a</td><td>NDB no</td></tr>
<tr class="even"><td>type</td><td>n</td><td>b (basic)</td><td>Report type: [b]asic or [f]ull or [s]tats</td></tr> 
<tr class="odd"><td>format<sup>1</sup></td><td>n</td><td>JSON</td><td>Report format: xml or json</td></tr>
</table>
<sup>1</sup>Format can also be sent in the request header:  Content-Type: application/json or Content-Type:application/xml.   

## Response Elements

A response can be lengthy but it's structure is relatively simple consisting of basic metadata for a food such as it's name, the food group to which belongs, scientific name and so on and a list of nutrients and nutrient values.  For each nutrient in the list, some metadata is provided such as name and the unit in which it is measured and it's value expressed in 100g.  Nutrients will also have a list of measures which are values of the nutrient at various portions, e.g. 1 cup.  Measures vary by food and nutrient.  Nutrients may also have a list of reference sources which are usually bibliographic citations in a non-standard format. 
 
<table>
<tr>
<th style="font-style:italic">report</th><th colspan="2">basic information about the report</th></tr>  
</tr>
<tr><td></td><td style="font-style:italic">type</td><td> Report type </td></tr> 
<tr class="odd"><td></td><td style="font-style:italic">sr</td><td>Release version of the data being reported</td></tr>  
<tr>
<th style="font-style:italic">food</th><th colspan="2">metadata elements for the food being reported</th></tr>  
<tr class="odd"><td></td><td style="font-style:italic">ndbno</td><td>  NDB food number </td></tr>  
<tr><td></td><td style="font-style:italic">name</td><td> food name </td></tr> 
<tr class="odd"><td></td><td style="font-style:italic">sd</td><td> short description </td></tr> 
 <tr  ><td></td><td style="font-style:italic">group </td><td> food group</td></tr>
<tr class="odd"><td></td><td style="font-style:italic">sn</td><td> scientific name</td></tr>
<tr ><td></td><td style="font-style:italic">cn </td><td> commercial name</td></tr>
 <tr class="odd"><td></td><td style="font-style:italic">manu </td><td> manufacturer</td></tr>   
 <tr><td></td><td style="font-style:italic">nf</td><td> nitrogen to protein conversion factor </td></tr>
  <tr class="odd"><td></td><td style="font-style:italic">cf</td><td> carbohydrate factor </td></tr>   
 <tr><td></td><td style="font-style:italic">ff</td><td> fat factor </td></tr>  
 <tr class="odd"><td></td><td style="font-style:italic">pf</td><td> protein factor</td></tr> 
<tr ><td></td><td style="font-style:italic">r</td><td> refuse %</td></tr>  
 <tr class="odd"><td></td><td style="font-style:italic">rd</td><td> refuse description</td></tr>
 <tr><td></td><td style="font-style:italic">ds</td><td>database source: 'Branded Food Products' or 'Standard Reference'</td></tr>
 <tr class="odd"><td></td><td style="font-style:italic">ru</td><td>reporting unit: nutrient values are reported in this unit, usually gram (g) or milliliter (ml)</td></tr>
 
 <tr><th >ing</th><th  colspan="2">ingredients (Branded Food Products report only)</th></tr> 
 <tr><td></td><td><i>desc</i></td><td> list of ingredients</td></tr>  
 <tr><td></td><td><i>upd</i></td><td>date ingredients were last updated by company</td></tr>  
 <tr><th >nutrient </th><th colspan="2">metadata elements for each nutrient included in the food report</td></tr>   
 <tr class="odd"><td></td><td style="font-style:italic">nutrient_id </td><td> nutrient number (nutrient_no) for the nutrient</td></tr>
 <tr><td></td><td style="font-style:italic">name </td><td> nutrient name</td></tr>     
  <tr class="odd"><td></td><td style="font-style:italic">sourcecode</td><td> list of source id's in the sources list referenced for this nutrient</th></tr>   
 <tr><td></td><td style="font-style:italic">unit</td><td> unit of measure for this nutrient</td></tr>  
 <tr class="odd" ><td></td><td style="font-style:italic" >value</td><td> 100 g equivalent value of the nutrient </td></tr>  
  <tr><td></td><td style="font-style:italic">dp</td><td># of data points</td>   
  <tr class="odd"><td></td><td style="font-style:italic">se</td><td> standard error </td></tr>
   <tr ><td></td><td style="font-style:italic">derivation</td><td>Indicator of how the value was derived</th></tr>   

  <tr><th>measures </th><th  colspan="2"> list of measures reported for a nutrient</th></tr>  
  <tr class="odd"><td></td><td style="font-style:italic">label</td><td> name of the measure, e.g. "large"</td></tr> 
 <tr><td></td><td style="font-style:italic">eqv </td><td> equivalent of the measure expressed as an eunit</td></tr>
 <tr class="odd"><td></td><td style="font-style:italic">eunit</td><td>Unit in with the equivalent amount is expressed.  Usually either gram (g) or milliliter (ml)</td></tr>
 
  <tr class="odd"><td></td><td style="font-style:italic">value </td><td> gram equivalent value of the measure </td></tr>  
<tr><th > source </th><th  colspan="2"> reference source, usually a bibliographic citation, for the food </th></tr>   
<tr class="odd"><td></td><td style="font-style:italic">title</td><td> name of reference</td></tr>
 <tr><td></td><td style="font-style:italic">authors</td><td> authors of the report</td></tr>
 <tr class="odd"><td></td><td style="font-style:italic">vol</td><td> volume </td></tr> 
 <tr><td></td><td style="font-style:italic">iss</td><td> issue  </td></tr>   
  <tr class="odd"><td></td><td style="font-style:italic">year</td><td> publication year </td></tr>  
  <tr><td></td><td style="font-style:italic">start </td><td> start page </td></tr> 
  <tr class="odd"><td></td><td style="font-style:italic">end</td><td> end page  </td></tr>
<tr><th colspan="3" > footnote</th></tr>    
  <tr><td></td><td style="font-style:italic">idv</td><td> footnote id</td></tr> 
 <tr class="odd"><td></td><td style="font-style:italic">desc</td><td>text of the foodnote</td></tr>        
<tr><th >langual</th><th  colspan="2"> LANGUAL codes assigned to the food </th></tr> 
 <tr class="odd"><td></td><td style="font-style:italic">code</td><td> LANGUAL code </td></tr> 
 <tr><td></td><td style="font-style:italic">desc </td><td> description of the code</td></tr>   
 </table>
          
## Some Examples  

#### XML 

Here's a couple of ways you can obtain the full report in XML format.   
Browser: https://api.nal.usda.gov/ndb/reports/?ndbno=01009&type=b&format=xml&api_key=DEMO_KEY   
CURL:  curl -H "Content-Type:application/xml" -d '&lt;report&gt;&lt;ndbno&gt;01009&lt;/ndbno&gt;&lt;type&gt;f&lt;/type>&lt;/report&gt;' DEMO_KEY@api.nal.usda.gov/usda/ndb/reports  

#### JSON   

Here's a couple of ways you can obtain the full report in JSON format.   
Browser: https://api.nal.usda.gov/ndb/reports/?ndbno=01009&type=b&format=json&api_key=DEMO_KEY
CURL:  curl -H "Content-Type:application/json" -d '{"ndbno":"01009","type":"f"}' DEMO_KEY@api.nal.usda.gov/ndb/reports  
