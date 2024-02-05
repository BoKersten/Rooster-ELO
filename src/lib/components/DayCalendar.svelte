<script>


	let date = new Date();
	$: day = date.getDate();
	const monthNames = ['januari', 'februari', 'maart', 'april', 'mei', 'juni', 'juli', 'augustus', 'september', 'oktober', 'november', 'december'];
	let month = date.getMonth();
	let today = new Date();
	$: hour = date.getHours();
    $: minutes = date.getMinutes();
	
	$: year = date.getFullYear();
	$: lastDayOfMonth = new Date(today.getFullYear(), month+1, 0).getDate();
	$: lastDayOfPrevMonth = new Date(today.getFullYear(), month, 0).getDate();
	
	const goToPrev = () => {
	day -= 1;
	if(day < 1){
		month -= 1;
		
		day = lastDayOfPrevMonth;
	}
	if(month == -1 /*if month is before january*/){
			
			month = 11; // set month equal to december
			year -= 1;
			
		}
	}
	
	const goToNext = () => {
	day += 1;
	
	if(day > lastDayOfMonth){
		month += 1;
		day = 1;
	}
	
	if(month == 12 /*if month is after december*/){
		month = 0; // set month to january
		year += 1; // up the year by one
	}
	}
	
	
	</script>


<main>

    <div class="day">
    
        <ul>
          <li class="prev" on:click={goToPrev}>&#10094;</li>
          <li class="next" on:click={goToNext}>&#10095;</li>
          <li>{day}<br>
            <span style="font-size:18px">{monthNames[month]}</span><br>
		<span style="font-size: 18px;">{year}</span>
		</li>
        </ul>
      </div>
      <ul class="timeline">
        
          <li>3:00</li>
          <li>6:00</li>
          <li>9:00</li>
          <li>12:00</li>
          <li>15:00</li>
          <li>18:00</li>
          <li>21:00</li>
          <li>00:00</li>

      </ul>

      <ul class="time h-80">
       {#if day == date.getDate()}
		 <!-- content here -->
		<div class="tooltip line" data-tip="{hour + ":" + minutes}" style="left: {hour * 4.16667 + minutes * 0.06944444444 + '%'};" id="line"></div>
	  
	{/if}
	</ul>
</main>




<style>


ul {list-style-type: none;}
	main {font-family: Verdana, sans-serif;}
	
	/* Month header */
	.day {
	  padding: 70px 25px;
	  width: auto;
	  background: #1abc9c;
	  text-align: center;
	}
    .day ul {
	  margin: 0;
	  padding: 0;
	}
	
	.day ul li {
	  color: white;
	  font-size: 20px;
	  text-transform: uppercase;
	  letter-spacing: 3px;
	}

    .day .prev {
	  float: left;
	  padding-top: 10px;
	  cursor: pointer;
	}
	
	/* Next button */
	.day .next {
	  float: right;
	  padding-top: 10px;
	  cursor: pointer;
	}

    .timeline {
	  margin: 0;
	  padding: 10px 0;
	  background-color:#ddd;
      width: 100%;
	}
	
	.timeline li {
	  display: inline-block;
	  border-right: solid;
	  color: #666;
	  text-align: center;
      width: 12.5%;
      font-size: 20px;
	}
	
    .time {
	  padding: 10px 0;
	  background: #eee;
	  margin: 0;
	  height: 250px;
      
	}

	.line{
		width: 1px;
		height: 100%;
		border-left: solid red 1px;
		position: relative;
	}
</style>