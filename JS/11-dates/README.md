<p>Creates a JavaScript Date instance that represents a single moment in time. Date objects are based on a time value that is the number of milliseconds since 1 January, 1970 UTC.</p>
<h5>Syntax</h5>
@CODE_START@@HTML@new Date();
new Date(value);
new Date(dateString);
new Date(year, month[, date[, hours[, minutes[, seconds[, milliseconds]]]]]);@CODE_END@
<h5>value</h5>
<p>Integer value representing the number of milliseconds since 1 January 1970 00:00:00 UTC, with leap seconds ignored (Unix Epoch; but consider that most Unix time stamp functions count in seconds).</p>
<h5>dateString</h5>
<p>String value representing a date. The string should be in a format recognized by the Date.parse() method</p>
<h5>year</h5>
<p>Integer value representing the year. Values from 0 to 99 map to the years 1900 to 1999</p>
<h5>date</h5>
<p>Optional. Integer value representing the day of the month.</p>
<h5>hours</h5>
<p>Optional. Integer value representing the hour of the day.</p>
<h5>minutes</h5>
<p>Optional. Integer value representing the minute segment of a time.</p>
<h5>seconds</h5>
<p>Optional. Integer value representing the second segment of a time.</p>
<h5>milliseconds</h5>
<p>Optional. Integer value representing the millisecond segment of a time.</p>
<h5>Description</h5>
<ul>
	<li>If no arguments are provided, the constructor creates a JavaScript Date object for the current date and time according to system settings.</li>
	<li>If at least two arguments are supplied, missing arguments are either set to 1 (if day is missing) or 0 for all others.</li>
	<li>The JavaScript date is based on a time value that is milliseconds since midnight 01 January, 1970 UTC. A day holds 86,400,000 milliseconds. The JavaScript Date object range is -100,000,000 days to 100,000,000 days relative to 01 January, 1970 UTC.</li>
	<li>The JavaScript Date object provides uniform behavior across platforms. The time value can be passed between systems to create a date that represents the same moment in time.</li>
	<li>Invoking JavaScript Date as a function (i.e., without the new operator) will return a string representing the current date and time.</li>
</ul>

<h5>Example on Date()</h5>

<section >  
    <div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
		onLoad: htmlcssjsContentOnLoaded,
		rendererOptions: { fontSize: 16 },
		advanced: { highlightActiveLine: true}
	}" style="min-height:300px;"><xmp><h3>Please open the console and see the log </h3>
<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
<!--try with different assignment operators like a ^= b, a |= b, a &= b etc. -->
<script language="javascript" type="text/javascript">
	var dat = Date();
	console.log("Date and Time : " + dat );
	
	var dt = new Date("December 25, 1995 23:15:00");
	console.log("getDate() : " + dt.getDate() );
	console.log("getDay() : " + dt.getDay() );
	console.log("getFullYear() : " + dt.getFullYear() ); 
 </script>
</xmp>
	</div>
	<div>
        <iframe id="preview"></iframe>
    </div>
</section>

<!--
@CODE_START@@HTML@<script type="text/javascript">
var dt = Date();
document.write("Date and Time : " + dt ); 
</script>@CODE_END@  
<div class="min-height-50" id="jsDateCode1"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsDateCode1','js')">Try Yourself</button></div>
<div class="output-panel"> 
<p>Date and Time : Tue Jan 31 2017 18:13:47 GMT+0530 (India Standard Time)</p>
</div>
<h5>Example on getDate()</h5>
@CODE_START@@HTML@<script type="text/javascript">
var dt = new Date("December 25, 1995 23:15:00");
document.write("getDate() : " + dt.getDate() ); 
</script>@CODE_END@  
<div class="min-height-50" id="jsDateCode2"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsDateCode2','js')">Try Yourself</button></div>
<div class="output-panel"> 
<p>getDate() : 25</p>
</div>
<h5>Example on getDay()</h5>
@CODE_START@@HTML@ <script type="text/javascript">
var dt = new Date("December 25, 1995 23:15:00");
document.write("getDay() : " + dt.getDay() ); 
</script>@CODE_END@  
<div class="min-height-50" id="jsDateCode3"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsDateCode3','js')">Try Yourself</button></div>
<div class="output-panel"> 
<p>getDay() : 1</p>
</div>
<h5>Example on getFullYear()</h5>
@CODE_START@@HTML@<script type="text/javascript">
var dt = new Date("December 25, 1995 23:15:00");
document.write("getFullYear() : " + dt.getFullYear() ); 
</script>@CODE_END@  
<div class="min-height-50" id="jsDateCode4"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsDateCode4','js')">Try Yourself</button></div>
<div class="output-panel"> 
<p>getFullYear() : 1995 </p>
</div>
<h5>Example on setDate()</h5>
@CODE_START@@HTML@<script type="text/javascript">
var dt = new Date( "Aug 28, 2008 23:30:00" );
dt.setDate( 24 );
document.write( dt );
</script>@CODE_END@  
<div class="min-height-50" id="jsDateCode5"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsDateCode5','js')">Try Yourself</button></div>
<div class="output-panel"> 
<p>Sun Aug 24 2008 23:30:00 GMT+0530 (India Standard Time) </p>
</div>

<h5>Example on setFullYear()</h5>
@CODE_START@@HTML@  <script type="text/javascript">
var dt = new Date( "Aug 28, 2008 23:30:00" );
dt.setFullYear( 2000 );
document.write( dt );
</script>@CODE_END@  
<div class="min-height-50" id="jsDateCode5"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsDateCode5','js')">Try Yourself</button></div>
<div class="output-panel"> 
<p>Mon Aug 28 2000 23:30:00 GMT+0530 (India Standard Time)</p>
</div>

<h5>Example on setMonth()</h5>
@CODE_START@@HTML@<script type="text/javascript">
var dt = new Date( "Aug 28, 2008 23:30:00" );
dt.setMonth( 2 );
document.write( dt );
</script>@CODE_END@  
<div class="min-height-50" id="jsDateCode6"><button type="button"  class="cws-button border-radius bt-color-3 pull-right" ng-click="tryYourSelf('jsDateCode6','js')">Try Yourself</button></div>
<div class="output-panel"> 
<p>Fri Mar 28 2008 23:30:00 GMT+0530 (India Standard Time)</p>
</div>

-->


