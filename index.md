<! DOCTYPE html>
<html>
<style>
#output{
 font-size:20px;
}
</style>
<head>
<title> Job Status </title>
<meta charset="UTF-8">
<meta name="author" content="Beth Allmon">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<br>

<label for="Job Number"> Enter the job number: </label>
<input type="text" name="Job Number" id="Job Number">

<br>
<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/4.1.2/papaparse.min.js"></script>
<input type="file" name="File Upload" id="txtFileUpload" accept=".csv"/>



<p id="output"> </p>

<script>
document.getElementById('txtFileUpload').addEventListener('change', upload, false);
 
 function upload(evt) {
	var data;
	var file = evt.target.files[0];
	var reader = new FileReader();
	reader.readAsText(file);
	reader.onload = function(event) {
		var csvData = event.target.result;
		
		data = Papa.parse(csvData, {header : false, complete: function(results) {callBack(results.data);}});
		
		console.log(data);
		
	};
	reader.onerror = function() {
		alert('Unable to read ' + file.fileName);
	};
	
  ;}
function callBack(data){
	var val = String(document.getElementById('Job Number').value);
	console.log(val);
	var string1=val.replace(/-/g,"");
	var result=null;
	for(i=0;i<data.length; i++){
	var val2 = String(data[i][0]);
	var string2 = val2.replace(/-/g,"");
		if (string1.localeCompare(string2)==0){
			result=data[i][1];	
		}
	}
	if(result==null){ document.getElementById('output').innerHTML='Please enter a valid job number';}
	else if(result==""){document.getElementById('output').innerHTML='Unknown Status';}
	
	else {document.getElementById("output").innerHTML='CURRENT STATUS: ' + result;}
}


</script>


</html>
