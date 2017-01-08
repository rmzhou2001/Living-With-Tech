+++
date = ""
title = "Reminder"

+++
<script language="JavaScript">
	 function saveReminder()
	  {
	   	  
	   var val = document.getElementById("reminder").value;
	   var exp = new Date(year, month, day);
	   exp.setDate(exp.getDate()+2);
	   var expires = "; expires=" + exp.toGMTString();
	   document.cookie = reminderDay + "=" + val + expires + "; path=/";
	   alert("Your reminder has been saved");
	   window.location="../Calendar";
	  }

	  function readCookie(name) {
		var nameEQ = name + "=";
		var ca = document.cookie.split(';');
		for(var i=0;i < ca.length;i++) {
			var c = ca[i];
			while (c.charAt(0)==' ') c = c.substring(1,c.length);
			if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length,c.length);
		}
		return "";
	}
	function createCookie(name,value,days) {
		if (days) {
			var date = new Date();
			date.setDate(date.getDate() + days);
			var expires = "; expires=" + date.toGMTString();
		}
		else var expires = "";
		document.cookie = name + "=" + value + expires + "; path=/";
	}
	function deleteCookie() {
		if (confirm("Do you wish to delete this reminder")) {
          createCookie(reminderDay,"",-1);
        }
		window.location="../Calendar";
	}
</script>
<a href="javascript:saveReminder();"><img src="../save.gif" class="icon" />Save Reminder&nbsp;&nbsp;|&nbsp;&nbsp; </a>
<a href="../Calendar"><img src="../cancel.gif" class="icon" />Cancel&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;</a>
<a href="javascript:deleteCookie();"><img src="../delete.gif" class="icon" />Delete Reminder</a>

<table>
	<tr>
		<td>
			Enter Reminder: 
		</td>
	</tr>
	<tr>
		<td>
			<input type="text" id="reminder" size="120"></input> 
		</td>
	</tr>
</table>
<script language="JavaScript">
    var parameters = location.search.substring(1).split("&");
    var temp = parameters[0].split("=");
	var year = unescape(temp[1]);
	temp = parameters[1].split("=");
	var month = unescape(temp[1]);
	temp = parameters[2].split("=");
	var day = unescape(temp[1]);
	var reminderDay = "d"+year+month+day;
	var today = new Date();
	var date = new Date(year, month, day);
	date.setDate(date.getDate()+1);
	if (date < today) {
		alert("This day already passed");
		window.location="../Calendar";
	} else {
		var cookieValue = readCookie(reminderDay);
		document.getElementById("reminder").defaultValue = cookieValue;
	}

</script>
