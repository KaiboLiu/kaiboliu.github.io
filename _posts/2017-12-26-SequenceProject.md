---
layout: post
title: Memo for Sequence Project
date: 2017-12-26 22:16:25 -0800
---

# CONTENTS
- [2017 Fall](#2017-fall)  
    - [RNA web demo (->)](#rna-web-demo)  
    - [Pseudoknot (->)](#pseudoknot)  
    
## 2017 Fall

## RNA web demo  
- [12/05/2017 - Task Initiallization](#12052017-tue)  
- [12/06/2017 - Getting Familiar](#12062017-wed)  
- [12/07/2017 - Layout](#12072017-thu)  
- [12/10/2017 - Rearrange Data by Seq](#12102017-sun)   
- [12/11/2017 - Learn JavaScript to draw](#12112017-mon)   
- [12/12/2017 - jQuery night](#12122017-tue)   
- [12/13/2017 - File Reading Problem](#12132017-wed)   
- [12/14/2017 - Staged Success](#12142017-thu)   
- [12/26/2017 - Fully Functioned](#12262017-tue)
- [***Back to CONTENTS***](#contents)  


#### 12/05/2017 Tue
Meeting with Prof. Huang and Dezhong, on the project of RNA sequence pairing.
RNA paring for pseudoknot-free mode is perfectly improved in linear solution. Next step is to optimize different types of crossing, from \\(O(n^3)\\) to \\(O(n^6)\\), to linear.  
The group also needs a web demo for visual illustration, especially for beam tunning. So I took the task for web development. Everything needs to study from the very beginning. 


[***Back*** to subcontents ***RNA web demo***](#rna-web-demo)

#### 12/06/2017 Wed
Check `RNA_visual` at Dezhong's file on ironcreek: `ssh liukaib@ironcreek.eecs.oregonstate.edu
`. Then copy them to my local:
```sh
scp -r liukaib@ironcreek.eecs.oregonstate.edu:/scratch/dengde/RNA_visual /Users/zhangyilin/0_pipi/LKB_OSU/Research/RNA
```
Borrow the source code from Vienna RNAfold WebServer. I need to modify many contents then deploy html file to my own webpage on engr:
```sh
# at OSU
scp /Users/zhangyilin/0_pipi/LKB_OSU/Research/RNA/web_demo/RNA_pair_web.html liukaib@flop.engr.oregonstate.edu:/nfs/stak/users/liukaib/public_html
# out of OSU
scp -r /Users/zhangyilin/0_pipi/LKB_OSU/Research/RNA/web_demo/rearranged_results/ liukaib@flop.engr.oregonstate.edu:/nfs/stak/users/liukaib/public_html
```
[***Back*** to subcontents ***RNA web demo***](#rna-web-demo)


#### 12/07/2017 Thu

Layout:
```
graph LR
contrafold-->contrafold_linear
vienna-->vienna_linear
```


[***Back*** to subcontents ***RNA web demo***](#rna-web-demo)

#### 12/10/2017 Sun
In Dezhong's `README`, data are listed like this:
```
Original data (sequences):
Mathewsdata.16s.seq
Mathewsdata.23s.seq

Gold:
Mathewsdata.16s.ref
Mathewsdata.23s.ref

Contrafold result:
Mathewsdata.16s.contrafoldres
Mathewsdata.23s.contrafoldres

Vienna result:
Mathewsdata.16s.viennares
Mathewsdata.23s.viennares

Linear Parser result using Contrafold model:
linearcontrafold/run_16s/*
linearcontrafold/run_23s/*

Linear Parser result using Vienna model:
linearvienna/run_16s/*
linearvienna/run_23s/*
```

Finishing `rearrange_by_seq.py`, rearrangement of pairing, put all the results of a single sequence (#4 of 16s, for example) into a data file, named `combine_16s.seq04`.  
There are always 1656 lines(seq\*2 + ref\*2 + cf\*2 + vn\*2 + linearcf\*206\*4 + lineavnf\*206\*4) in each data file if category of beams is 206 (1,2,..200,300,..,800).  


The structure of the file is:  
```
seq * 2 lines		    ----->  L1
ref * 2 lines		    ----->  L3
cf  * 2 lines		    ----->  L5
vn  * 2 lines 		    ----->  L7
linearcf.beam001 * 4 lines  ----->  L11 (with 2 lines of information above)
lineavnf.beam001 * 4 lines  ----->  L16 (with 2 lines of information above)
linearcf.beam002 * 4 lines
lineavnf.beam002 * 4 lines
...
linearcf.beam00i * 4 lines  ----->  L(8*i+3) (with 2 lines of information above), if i > 200, L[(i/100+198)*8+3]
lineavnf.beam00i * 4 lines  ----->  L(8*i+7) (with 2 lines of information above), if i > 200, L[(i/100+198)*8+7]
```
通宵

[***Back*** to subcontents ***RNA web demo***](#rna-web-demo)


#### 12/11/2017 Mon
Think about methods to make javascript to read data files like `combine_16s.seq04` to draw graph.  
半通宵


[***Back*** to subcontents ***RNA web demo***](#rna-web-demo)

#### 12/12/2017 Tue
```javascript
jQuery.get( url [, data ] [, success(data, textStatus, jqXHR) ] [, dataType ] )
```
描述: 使用一个HTTP GET请求从服务器加载数据。  
It's an abbreviation of ajax, equalent to:
```javescript
$.ajax({
  url: url,
  data: data,
  success: success,
  dataType: dataType
});
```
Usage:
```
jQuery.get('http://localhost/foo.txt', function(data) {
    var myvar = data;
});
```
ps: `jQuery.get()=$.get()`


##### HTML:  
element: a pair of tags and all those between it
- has closing tag: `<h1>`, `<button>`, `<a>`, `<div>`, `<body>`, `<html>`
- closing tag is optional: `<p>`, `<option>`;
- no closing tag: `<br>`, `<img>`
 

attribute: in the openning tag(`class`, `id`, `style`, `title`, `lang`)  

class 属性可以多用 class=" " （引号里面可以填入多个class属性）  
id 属性只能单独设置 id=" "（只能填写一个，多个无效）  

##### jQuery selector:  
element selector `$("p")`  
id 选择器 `$(#id)`  
class 选择器 `$(.class)`  

[***Back*** to subcontents ***RNA web demo***](#rna-web-demo)

#### 12/13/2017 Wed
Solved an interested problem:
When I use `$.get()`, the URL should be an open access domain, otherwise there will be an error `No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'null' is therefore not allowed access.`.  
The browser usually allows a request in the same origin for security reasons. `CORS` is designed for cross-domain request. Or simply without `CORS`:
- If I want to `$.get()` a file on server, the html file should also be run on the server.
- If I want to `$.get()` a file on github, I can run html both locally or on server.
 
```
$(document).ready(function(){
   // jQuery...
});
```
is equivalent to 
```
$(function(){
   // jQuery...
});
```
[***Back*** to subcontents ***RNA web demo***](#rna-web-demo)

#### 12/14/2017 Thu
Use `json.dump(a:b)` in python and `$.getJSON(URL,function(data){...})` in js, to make file data reable for html.  

But I cannot pass variables out in this getJSON.  
This happens because that callback function (function(data) {...}) runs later when the response comes back...because it's an asynchronous function. Instead use the value once you have it set, like this:
...

After finishing all the configuration, I can draw 4 beautiful graphs for a default data file(a specific sequence) on the webpage.  
Transfer `html`, `js`, `arc_pairing_json.py`, `rearrange_by_seq.py`, and data file `pairing_for_js` to server:
```
scp /Users/zhangyilin/0_pipi/LKB_OSU/Research/RNA/web_demo/arc_pairing_json.py liukaib@flop.engr.oregonstate.edu:/nfs/stak/users/liukaib/public_html/
scp /Users/zhangyilin/0_pipi/LKB_OSU/Research/RNA/web_demo/demo_myScript.js liukaib@flop.engr.oregonstate.edu:/nfs/stak/users/liukaib/public_html/
scp /Users/zhangyilin/0_pipi/LKB_OSU/Research/RNA/web_demo/demo_json+canvas.html liukaib@flop.engr.oregonstate.edu:/nfs/stak/users/liukaib/public_html/
scp -r /Users/zhangyilin/0_pipi/LKB_OSU/Research/RNA/web_demo/pairing_for_js/ liukaib@flop.engr.oregonstate.edu:/nfs/stak/users/liukaib/public_html/
scp /Users/zhangyilin/0_pipi/LKB_OSU/Research/RNA/web_demo/rearrange_by_seq.py liukaib@flop.engr.oregonstate.edu:/nfs/stak/users/liukaib/public_html/
```

My demo is available on `http://web.engr.oregonstate.edu/~liukaib/demo_json+canvas.html`. I sent an email to my boss for my update.  
凌晨7点睡。

[***Back*** to subcontents ***RNA web demo***](#rna-web-demo)

#### 12/26/2017 Tue
Start working at midnight.
Add the functionality of slide bar value call back, then extract seq series and seq number from seletion.  
Learn the usage of `<span>`, interesting.  
The final demo can be found at [my OSU homepage](http://web.engr.oregonstate.edu/~liukaib/demo_json+canvas.html).

Finish the work at 5:50am.

[***Back*** to subcontents ***RNA web demo***](#rna-web-demo)