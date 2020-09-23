<div align="center">

## VBScript's DateSerial Function


</div>

### Description

DateSerial is a function that is supplied in VBScript, and Javascript doesn't have a function like this, so I created a function to work in Javascript to do the same as the VBScript function does. I hope you all find this useful. I'm working on a hold Script Library with all the VBScript Functions converted into Javascript. I'm about 90% Completed.
 
### More Info
 
Year, Month, Day

Date in the format as MM/DD/YYYY

None, that are know of.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Randy McCleary](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/randy-mccleary.md)
**Level**          |Advanced
**User Rating**    |4.9 (44 globes from 9 users)
**Compatibility**  |
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__2-57.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/randy-mccleary-vbscript-s-dateserial-function__2-3637/archive/master.zip)





### Source Code

```
/**************************************************************
 DateSerial: This function returns the current Date of the computer.
 Parameters:
   Year : String, Integer, or Expression (100 To 9999)
   Month : String, Integer, or Expression (-9999999 To +9999999)
   Day  : String, Integer, or Expression (-9999999 To +9999999)
 Returns: Returns the Date. (6/22/2003)
***************************************************************/
function DateSerial(Year, Month, Day) {
	var Years  = new Number(Year);
	var Months = new Number(Month);
	var Days  = new Number(Day);
	var arrDays = new Array(31,28,31,30,31,30,31,31,30,31,30,31);
	//***************************************************
	// Years
	//***************************************************
	if ((Years >= 100) && (Years <= 9999)) {
		Years = Years;
	}
	else {
		return null;
	}
	//***************************************************
	// Months
	//***************************************************
	if (Months >= 1 && Months <= 12) {
		Months = Months;
	}
	else if (Months > 12) {
		// While Months is greater than 12, then keep subtracting 12
		// to Months and incrementing the year by one.
		while (Months > 12 ) {
			Months -= 12;
			Years += 1;
		}
	}
	else if (Months < 1) {
		// While Months is less than - 12, then keep adding 12 to Months
		// and decrementing the year by one.
		while (Months <= -12 ) {
			Months += 12;
			Years -= 1;
		}
		// If Months is greater than -12 and is Greater or Equal to 0
		// then subtract One from Years.
		if (Months > -12 && Months <= 0) {
			Years -= 1;
		}
		// Months = 12 plus what is left over in the variable Months
		Months = 12 + Months;
	}
	//***************************************************
	// Days
	//***************************************************
	if (Days > 0) {
		// Set DaysInMonth for Feburary
		arrDays[1] = DaysInMonth(2, Years);
		// While Days is greater than the total days in the month subtract
		// the total days from the Days, and increment the Months by 1.
		while (Days > arrDays[Months - 1]) {
			Days -= arrDays[Months -1];
			Months += 1;
			if (Months > 12) {
				Months -= 12;
				Years += 1;
			}
			// Set DaysInMonth for Feburary
			arrDays[1] = DaysInMonth(2, Years);
		}
	}
	else if (Days <= 0) {
		if (Days == 0) {
			Months -=1;
			if (Months == 0){
				Months = 12;
				Years -= 1;
			}
			// Set DaysInMonth for Feburary
			arrDays[1] = DaysInMonth(2, Years);
			Days = arrDays[Months-1];
		}
		else {
			arrDays[1] = DaysInMonth(2, Years);
			// While Days is less than or equal to the total days in the Month
			// then increment the days by the total days in the month and
			// subtract one from the Months.
			while (Days <= - arrDays[Months - 1]) {
				// Set DaysInMonth for Feburary
				arrDays[1] = DaysInMonth(2, Years);
				Days += arrDays[Months -1];
				Months -= 1;
				if (Months == 0) {
					Months += 12;
					Years -= 1;
				}
				// Set DaysInMonth for Feburary
				arrDays[1] = DaysInMonth(2, Years);
			}
			if (Days == 0 || Days > -arrDays[Months-1]) {
				Months -=1;
			}
			if (Months == 0) {
				Months += 12;
				Years -= 1;
			}
			// Set DaysInMonth for Feburary
			arrDays[1] = DaysInMonth(2, Years);
			if (Days == -arrDays[Months-1]) {
				Days = 0;
				Months -=1;
			}
			if (Months == 0) {
				Months += 12;
				Years -= 1;
			}
			// Set DaysInMonth for Feburary
			arrDays[1] = DaysInMonth(2, Years);
			// Days is equal to the number of days in the month to
			// the days left over not greater then the total days
			// in the month. Ex: Jan 31 days - 15 = Jan 16th.
			Days = arrDays[Months-1] + Days;
		}
	}
	if ((Years >= 1) && (Years <= 9999)) {
		return Months + "/" + Days + "/" + Years;
	}
	else {
		return null;
	}
}
/**************************************************************
 DaysInMonth: This function returns the number of days in a
 	      a given month and year. This is used to find out
 	      when a year has a leap day or not.
 Parameters:
  Month = A month Number (1-12).
  Year = A 4 Digit Year number.
 Returns: Integer - (28-31).
***************************************************************/
function DaysInMonth(Month, Year) {
	var Days;
	var arrDays = new Array(31,28,31,30,31,30,31,31,30,31,30,31);
	if ((Month==2) && (Year % 4 == 0 && (Year % 100 != 0 || Year % 400 == 0))) {
		arrDays[1] = 29;
	}
	return arrDays[Month-1];
}
```

