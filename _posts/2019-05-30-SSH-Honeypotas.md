---
title: SSH Honeypotas
published: true
---

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>

<p>Iveskite SSH duomenis:</p>
<input type="text" id="textbox">
<table id="table"></table>
<div>

</div>
<script>
	var PopPassword;
	var textbox = document.getElementById("textbox");
	var table = document.getElementById("table");

	function OnTextBoxChange() {
		while (table.firstChild) {
			table.removeChild(table.firstChild);
		}
		if(textbox.value!="") {
			var maxResults = 50;
			for(var k in PopPassword) {
				if(k.startsWith(textbox.value)) {
					var tr = document.createElement('tr');   

					var td1 = document.createElement('td');
					var td2 = document.createElement('td');

					var text1 = document.createTextNode(k);
					var text2 = document.createTextNode(PopPassword[k]);

					td1.appendChild(text1);
					td2.appendChild(text2);
					
					tr.appendChild(td1);
					tr.appendChild(td2);

					table.appendChild(tr);
					if(maxResults > 0){
						maxResults--;
					}
					else{
						break;
					}
				}
			}
		}
		
	}

	function LoadJsonFiles() {
		var xmlhttp = new XMLHttpRequest();
		xmlhttp.onreadystatechange = function() {
			if (this.readyState == 4 && this.status == 200) {
				PopPassword = JSON.parse(this.responseText);
			}		
		};
		xmlhttp.open("GET", "https://raw.githubusercontent.com/tomasvanagas/S-in-IOT-stands-for-security/master/cowrie/PopUserpass.json", true);
		xmlhttp.send();
	}

	LoadJsonFiles();
	document.getElementById("textbox").addEventListener('input', OnTextBoxChange);
</script>
