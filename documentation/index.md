AGCalendar Module <img src="http://f.cl.ly/items/422Q2T3G043h0O171E1z/acgLogo.png" height="35" valign="bottom" />
============
## Description
AGCalendar enables you to access the native calendar on your iPhone, iPad or iPod. EventKit and Core Data are both supported data sources. This enables you to switch between iCal and your custom calendar. Some more information below.

* **EventKit**: All events including the events in your native calendar will be shown. Events added will also be added to your native iCal.
* **CoreData**: Uses Core Data to store your calendar-events. Only events added by your application will be shown. Added events will not be added to iCal. This also allows you to add more details to your events. 

> <img src="http://f.cl.ly/items/1h3O0S3p2T0f1K2G2h1w/info1.png" height="228" style="margin-right:20px;" />


Accessing the Calendar Module
--------------------------

To access this module from JavaScript, you would do the following:

>     Titanium.Calendar = Ti.Calendar = require("ag.calendar");

Functions
--------
## `Ti.Calendar.dataSource(ids[string])`
This will set the data source you want to use.    
If this is not set, the calendar will default to EventKit as your data source.     

Please read the  *description* above for more information.

### Argument
* [string] **dataSource**: *eventkit* or *coredata* (Default: eventkit)

### Example
>     Ti.Calendar.dataSource("coredata");

## `Ti.Calendar.createView(object)`
This will create a calendarView with controls to move back an forth between months.

### Arguments
* [boolean] **editable**: Turns "swipe-to-delete" on or off. Defaults to  *false*
* [string] **color**: This is required by Titanium for some reason. Just set it to "*white*"

### Example
>     var calendarView = Ti.Calendar.createView({
		top: 0,
		editable: true,
		color: "white"
	});



## `Ti.Calendar.addEvent(object)`
This will add an event to your calendar object.
### Parameters
* **EventKit**   

 * [string] **title**: Event title
 * [string] **location**: Events location.
 * [string] **note**: Event notes.
 * [date] **startDate**: Events start. (Javascript date object)
 * [date] **endDate**: Events end. (Javascript date object) 
 * [object] **recurrence**: Recurrence rule (**EventKit only**)

* **Core Data** (Including the above)      

 * [string] **type**: Event type. E.g: *public* or *private*
 * [string] **attendees**: Comma-separated list of attendees
 * [string] **identifier**: Event identifier.
 * [string] **organizer**: Name of the organizer

### Example
>     var endDate = new Date();
	endDate.setHours(endDate.getHours()+3); // Set event to last 3 hours.

>     // Date to end our recurring event
	var recurringEnd = new Date();
	recurringEnd.setMonth(recurringEnd.getMonth()+6); // Recurring ends in 6 months

>     calendar.addEvent({
        title: "Attend the 2011 WWDC conference",   
        startDate: new Date(),  
        endDate: endDate,   
        location: "San Francisco",   
        identifier: Ti.Calendar.identifier,
        type:"public",
        attendees: "Steve, Phil",
        organizer: "Chris Magnussen",
        note: "Be mad about not getting the iPhone 5",
        recurrence: {
	         frequency: "month", // day, week, month, year
	         interval: 1,
	         end: recurringEnd
        }
    });

## `calendarView.selectTodaysDate([void])`
Select todays date in the calendarView.     
Nothing more, nothing less..

### Example

>     var calendarView = Ti.Calendar.createView();
>     var todayButton = Ti.UI.createButton({title: "Today"});

>     todayButton.addEventListener("click", function() {
        calendarView.selectTodaysDate();
    });

>     window.setLeftNavButton(todayButton);

Properties
--------
## `Ti.Calendar.identifier (read-only)`

This can be used for the ***identifier***-parameter in the *createView()*-instance. 

### Returns
* [string] MD5 sum of globallyUniqueString

Events
-----
## `event:clicked`
When adding this to the calendar-view you will get all event-data in a single array whenever a user clicks the event-table.

### Returns
* [string] **title**
* [string] **type** (*)
* [string] **location**
* [string] **attendees** (*)
* [string] **description** (*)
* [string] **identifier** (**)
* [string] **organizer** (*)
* [date] **startDate** (Standard dateTime format)
* [date] **endDate** (Standard dateTime format)

(\*) Only available when using Core Data as the data source.   
(\**) When using Core Data your custom identifier is returned, else the auto generated eventIdentifier in EventKit is returned.

### Example
>     calendarView.addEventListener("event:clicked", function(e) {
        var event = e.event;
        var start_date = new Date(event.startDate);
        alert(event.title+" will start "+start_date);
    });


## Usage

See example.

## Author

Chris Magnussen for Appgutta, DA.

 * [Twitter][]
 * [Appgutta.no][]

License
------
Copyright(c) 2012 by Appgutta, DA. All Rights Reserved. Please see the LICENSE file included in the distribution for further details.


[Twitter]: http://twitter.com/crmag
[Appgutta.no]: http://www.appgutta.no
