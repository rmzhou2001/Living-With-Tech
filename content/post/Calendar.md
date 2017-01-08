+++
date = ""
title = "Calendar"

+++

<script type="text/javascript">
<!--  to hide script contents from old browsers
function encode (str) {
  var dest = "";
  var len = str.length;
  var index = 0;
  var code = null;
  for (var i = 0; i < len; i++) {
    var ch = str.charAt(i);
    if (ch == " ") code = "%20";
    else if (ch == "%") code = "%25";
    else if (ch == ",") code = "%2C";
    else if (ch == ";") code = "%3B";
    else if (ch == "\b") code = "%08";
    else if (ch == "\t") code = "%09";
    else if (ch == "\n") code = "%0A";
    else if (ch == "\f") code = "%0C";
    else if (ch == "\r") code = "%0D";
    if (code != null) {
      dest += str.substring(index,i) + code;
      index = i + 1;
      code = null;
    }
  }
  if (index < len)
    dest += str.substring(index, len);
  return dest;
}
function decode (str) {
  var dest = "";
  var len = str.length;
  var index = 0;
  var code = null;
  var i = 0;
  while (i < len) {
    i = str.indexOf ("%", i);
    if (i == -1)
      break;
    if (index < i)
      dest += str.substring(index, i);
    code = str.substring (i+1,i+3);
    i += 3;
    index = i;
    if (code == "20") dest += " ";
    else if (code == "25") dest += "%";
    else if (code == "2C") dest += ",";
    else if (code == "3B") dest += ";";    
    else if (code == "08") dest += "\b";
    else if (code == "09") dest += "\t";
    else if (code == "0A") dest += "\n";
    else if (code == "0C") dest += "\f";
    else if (code == "0D") dest += "\r";
    else {
      i -= 2;
      index -= 3;
    }
  }        
  if (index < len)
    dest += str.substring(index, len);
  return dest;
}
function arrayOfDaysInMonths(isLeapYear)
{
   this[0] = 31;
   this[1] = 28;
   if (isLeapYear)
   this[1] = 29;
   this[2] = 31;
   this[3] = 30;
   this[4] = 31;
   this[5] = 30;
   this[6] = 31;
   this[7] = 31;
   this[8] = 30;
   this[9] = 31;
   this[10] = 30;
   this[11] = 31;
}
function daysInMonth(month, year)
{
   var isLeapYear = (((year % 4 == 0) && (year % 100 != 0)) || (year % 400 == 0));
   var monthDays  = new arrayOfDaysInMonths(isLeapYear);
   return monthDays[month];
}
function calendar(day, month, year)
{
   var monthNames = "JanFebMarAprMayJunJulAugSepOctNovDec";
   var today      = new Date();
   if (month == '0') {
     today = new Date("January "+day+", "+year+" 00:00:00");
   }
   if (month == '1') {
     today = new Date("February "+day+", "+year+" 00:00:00");
   }
   if (month == '2') {
     today = new Date("March "+day+", "+year+" 00:00:00");
   }
   if (month == '3') {
     today = new Date("April "+day+", "+year+" 00:00:00");
   }
   if (month == '4') {
     today = new Date("May "+day+", "+year+" 00:00:00");
   }
    if (month == '5') {
     today = new Date("June "+day+", "+year+" 00:00:00");
   } 
   if (month == '6') {
     today = new Date("July "+day+", "+year+" 00:00:00");
   } 
   if (month == '7') {
     today = new Date("August "+day+", "+year+" 00:00:00");
   } 
   if (month == '8') {
     today = new Date("September "+day+", "+year+" 00:00:00");
   }
    if (month == '9') {
     today = new Date("October "+day+", "+year+" 00:00:00");
   }
    if (month == '10') {
     today = new Date("November "+day+", "+year+" 00:00:00");
   }
    if (month == '11') {
     today = new Date("December "+day+", "+year+" 00:00:00");
   }
   var numDays    = daysInMonth(month, year);
   var firstDay   = today;
       firstDay.setDate(1);
   var startDay = firstDay.getDay();
   var column = 0;
   document.write("<CENTER>");
   document.write("<TABLE BORDER>");
   document.write("<TR><TH COLSPAN=7>");
   document.write(monthNames.substring(3*month, 3*(month + 1)) + " " + year);
   document.write("</th></tr><TR><TH>Sun</th><TH>Mon</th><TH>Tue</th><TH>Wed</th><TH>Thu</th><TH>Fri</th><TH>Sat</th></tr>");

   document.write("<TR>");
   column = 0;
   for (i=0; i<startDay; i++)
   {
      document.write("<TD>&nbsp;</td>");
      column++;
   }
 
   for (i=1; i <= numDays; i++)
   {
      var s = "" + i;
      if ((readCookie("d"+year+month+i) != null)) 
        s = s.fontcolor("#FF0000");
      s = s.link("../reminder?year="+year+"&month="+month+"&day="+i);;
      document.write("<TD>" + s);
      if (++column == 7)
      {
         document.write("</tr><TR>"); // start a new row
         column = 0;
      }
      document.write("</td>");
   }
   document.write("</tr></TABLE>");
   document.writeln("</CENTER>");
}

function readCookie(name) {
		var nameEQ = name + "=";
		var ca = document.cookie.split(';');
		for(var i=0;i < ca.length;i++) {
			var c = ca[i];
			while (c.charAt(0)==' ') c = c.substring(1,c.length);
			if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length,c.length);
		}
		return null;
	}

// --> <!-- end hiding contents from old browsers  -->
</SCRIPT>

<SCRIPT LANGUAGE="JavaScript">
<!--  to hide script contents from old browsers
   var today = new Date();
   var day        = today.getDate();
   var month      = today.getMonth();
   var year       = today.getYear() + 1900;
  var numMonths = 3;
  for (k=0; k < numMonths; k++) {;
    if (month+k==12) {
      calendar(day,0,year+1);
    }
    else {
      calendar(day,month+k,year);
    } 
  }
// --> <!-- end hiding contents from old browsers  -->
</script>