Create Create Apex Class
Create a Unit Test for a Simple Apex Class
Create and install a simple Apex class to test if a date is within a proper range, and if not, returns a date that occurs at the end of the month within the range. You'll copy the code for the class from GitHub. Then write unit tests that achieve 100% code coverage.
Create an Apex class:
Name: VerifyDate
Code: Copy from GitHub
Place the unit tests in a separate test class:
Name: TestVerifyDate
Goal: 100% code coverageCreate a Unit Test for a Simple Apex Class
Create and install a simple Apex class to test if a date is within a proper range, and if not, returns a date that occurs at the end of the month within the range. You'll copy the code for the class from GitHub. Then write unit tests that achieve 100% code coverage.
Create an Apex class:
Name: VerifyDate
Code: Copy from GitHub
Place the unit tests in a separate test class:
Name: TestVerifyDate
Goal: 100% code coverage
Run your test class at least once

public class VerifyDate {

	//method to handle potential checks against two dates
	public static Date CheckDates(Date date1, Date date2) {
		//if date2 is within the next 30 days of date1, use date2.  Otherwise use the end of the month
		if(DateWithin30Days(date1,date2)) {
			return date2;
		} else {
			return SetEndOfMonthDate(date1);
		}
	}

	//method to check if date2 is within the next 30 days of date1
	private static Boolean DateWithin30Days(Date date1, Date date2) {
		//check for date2 being in the past
        	if( date2 < date1) { return false; }

        	//check that date2 is within (>=) 30 days of date1
        	Date date30Days = date1.addDays(30); //create a date 30 days away from date1
		if( date2 >= date30Days ) { return false; }
		else { return true; }
	}

	//method to return the end of the month of a given date
	private static Date SetEndOfMonthDate(Date date1) {
		Integer totalDays = Date.daysInMonth(date1.year(), date1.month());
		Date lastDay = Date.newInstance(date1.year(), date1.month(), totalDays);
		return lastDay;
	}

}

@istest
public class TestVerifyDate {
@istest static void testSameDate() {
System.assertEquals(
VerifyDate.CheckDates(Date.newInstance(2022, 10, 26),
Date.newInstance(2022, 10, 26)),
Date.newInstance(2022, 10, 26)
);
}
@istest static void testDateInversion() {
System.assertEquals(
VerifyDate.CheckDates(Date.newInstance(2022, 10, 26),
Date.newInstance(2022, 10, 25)),
Date.newInstance(2022, 10, 26)
);
}
@istest static void testMoreThan30DayDelta() {
System.assertEquals(
VerifyDate.CheckDates(Date.newInstance(2022, 08, 26),
Date.newInstance(2022, 10, 26)),
Date.newInstance(2022, 10, 26)
);
}
}





Create Apex Class
