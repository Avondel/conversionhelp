# conversionhelp

A simple "hand holder" to assist students in conversions.
<!DOCTYPE HTML>
<html>
   <head>
      <script type = "text/javascript">
     		//start/end is for the computer top/bottom is for the user
	
			function myReset() { 
				initiate();
			}
			
			function myFunction() {
				alert("Kitty");
			}
			
			function initiate() {
				startUnit = "Starting Units";
				endUnit = "Ending Units";
				startNum = 0;
				endNum = 0;
				flip = 0;
				
				topUnit = startUnit;
				topNum = startNum;
				bottomUnit = endUnit;
				bottomNum = endNum;
				
				document.getElementById('Step2a').innerHTML = startUnit; 
				document.getElementById('Step2b').innerHTML = endUnit;
				
				document.getElementById('Factor1').innerHTML = topNum + " " + topUnit; 
				document.getElementById('Factor2').innerHTML = bottomNum + " " + bottomUnit;
				
				document.getElementById('Step3').innerHTML = startUnit;
				
			}
			
			function labelUpdate() {
				if (document.forms["myform"]["startUnitForm"].value === "")
					startUnit = "Start Units";
				else
					startUnit = document.forms["myform"]["startUnitForm"].value;
				
				if (document.forms["myform"]["endUnitForm"].value === "")
					endUnit = "End Units";
				else
					endUnit = document.forms["myform"]["endUnitForm"].value;
					
				if (document.forms["myform"]["topNumForm"].value === "")
					startNum = 0;
				else
					startNum = document.forms["myform"]["topNumForm"].value;
				
				if (document.forms["myform"]["bottomNumForm"].value === "")
					endNum = 0;
				else
					endNum = document.forms["myform"]["bottomNumForm"].value;
				
				if ( flip === 0)	{
					topUnit = startUnit;
					topNum = startNum;
					bottomUnit = endUnit;
					bottomNum = endNum;
				}
				else	{
					topUnit = endUnit;
					topNum = endNum;
					bottomUnit = startUnit;
					bottomNum = startNum;
				}
				
				
				document.getElementById('Step2a').innerHTML = startUnit; 
				document.getElementById('Step2b').innerHTML = endUnit;
				
				document.getElementById('Factor1').innerHTML = topNum + " " + topUnit; 
				document.getElementById('Factor2').innerHTML = bottomNum + " " + bottomUnit;
				
				document.getElementById('Step3').innerHTML = startUnit;

			}
			
			function Flip() {
				if (flip === 0) 
					flip = 1;	//flipped
				else
					flip = 0;	//not flipped
				topUnitTemp = topUnit;
				topNumTemp = topNum;
				topUnit = bottomUnit;
				topNum = bottomNum;	
				bottomUnit = topUnitTemp;
				bottomNum = topNumTemp;
				document.getElementById('Factor1').innerHTML = topNum + " " + topUnit; 
				document.getElementById('Factor2').innerHTML = bottomNum + " " + bottomUnit;
			
			}
			
			function Check() {
				//Is everything filled in?
				flag = 0;
				errorMsg = "Please fill in: \n";

				startUnit = document.forms["myform"]["startUnitForm"].value;
				endUnit = document.forms["myform"]["endUnitForm"].value;
				topNum = document.forms["myform"]["topNumForm"].value;
				bottomNum = document.forms["myform"]["bottomNumForm"].value;
				numberStart = document.forms["myform"]["numberStartForm"].value;

				if ( startUnit === "")	{
					flag = 1;
					errorMsg += "Starting Units\n";
				}
				if ( endUnit === "")	{
					flag = 1;
					errorMsg += "Ending Units\n";
				}
				if ( topNum === "" )	{
				alert(topNum);
					flag = 1;
					errorMsg += "First Conversion Number\n";
				}
				
				if ( bottomNum === "")	{
					flag = 1;
					errorMsg += "Second Conversion Number\n";
				}
				if (numberStart === "")	{
					flag = 1;
					errorMsg += "Starting number from your problem.";
				}
				
				if (flag === 1)	{
					alert(errorMsg);
					return;
				}
				
				//Are there zeroes?
				
				flag = 0;
				errorMsg = "Please replace zeros with another number in: \n";
				
				if (topNum === "0" ){
					flag = 1;
					errorMsg += "First conversion number\n";
				}
				if (bottomNum === "0")	{
					flag = 1;
					errorMsg += "Second conversion number\n";
				}
				if (numberStart === "0")	{
					flag = 1;
					errorMsg += "Number from your problem.";
				}

				if (flag === 1)	{
					alert(errorMsg);
					return;
				}
				
				//Check for numeric entries.
				flag = 0;
				errorMsg = "Please use only numbers in: \n";
				if ( isNaN(topNum )	){
					flag = 1;
					errorMsg += "First conversion number\n";
				}
				if( isNaN( bottomNum ) ){
					flag = 1;
					errorMsg += "Second conversion number\n";
				}
				if( isNaN( numberStart )) {
					flag = 1;
					errorMsg += "Number from your problem.";
				}
				
				if (flag === 1) {
					alert(errorMsg);
					return;
				}

				//Is the conversion factor the right way up?
				flag = 0;
				if (bottomUnit !== startUnit)	{
					flag = 1;
					errorMsg = "Try flipping your conversion factor.";
				}
				
				if (flag ===1)	{
					alert(errorMsg);
					return;
				}
				
				if (flip ===1)	{
					topNumTemp = topNum;
					topNum = bottomNum;
					bottomNum = topNumTemp;
				}

				//Calculate what we think the answer is....
				myAnswer = numberStart * topNum / bottomNum;
				goodMsg = "I think the answer is: " + myAnswer;
				alert(goodMsg);
			}
			
				
			
     </script>
   </head>
   
   <body onload = "initiate()">
	<!-- start/end is computer. top/bottom is for the user. /!-->
		
		<center><h2>Unit Conversion Helper</h2></center>
		<p>This is intended for single step unit conversion problems.</p>
				
		<form action = "/cgi-bin/html5.cgi" method = "get" name = "myform" >		
		<table border = "1">
			<tr>
				<td>		<p id="Step1"></p>
					<h3>Step 1: Read the problem and note what units you are working with.</h3>
						Starting Units : <input type = "text" name = "startUnitForm" onblur = "labelUpdate()" required /> &nbsp 
						Ending Units: <input type = "text" name = "endUnitForm" onblur = "labelUpdate()" required /><br><br>
						<p>(Hint: If you are having difficulty, please read the problem and note the units used.</p>
				</td>
			</tr><tr>
				<td>		<h3>Step 2: Set up the conversion factor</h3>
			<input type = "text" name = "topNumForm" onblur = labelUpdate() required />
					<label id="Step2a"><output> &nbsp </output> </label>
			<big> &nbsp = &nbsp </big>
			<input type = "text" name = "bottomNumForm" onblur = labelUpdate() required />
					<label id="Step2b"><output> &nbsp </output> </label>
			<p>If you are having difficulty, the information is usually in the back of your physics or chemistry book.</p>
		<br></td>
			</tr></table>
		<table border = "2">
			<tr>
				<td colspan = "3">				<h3>Step 3: Solve</h3>
				<p>Enter the starting number in the first box and fill in the others from the Drop Down Boxes.<br>
					Then, multiply the numbers on the top and divide by the number on the bottom<br>
					Click "Check Work" to see if you agree with the machine.</p></td>
			</tr><tr>
				<td><input type = "text" name = "numberStartForm" required />
				<big><big>
				<label id="Step3"><output> &nbsp </output> </label>
				<big> * </big></big></big></td>
				<td>				
					<big><big><u>
					<label id='Factor1'><output name = "displayTop"> &nbsp </output></label></u> &nbsp &nbsp =<br>
					<label id='Factor2'><output name = "displayBottom"> &nbsp </output> </label/></big></big><br><br>
					<input type = "button" value = "Flip" onclick = "Flip();" /></td>
			</tr><tr>
				<td colspan = "2"><center><big><big>    
					<input type = "button" value = "Check Work"  onclick = "Check();" />
			<input type = "reset" onclick = "myReset();"/></td></big></big></center>
			</tr>
		</table>
		
		</form>

   </body>
</html>
