The Event class is the base class for all Event classes.When creating a custom Event, the Event should inherit from the Event class.The Event class also contains events. These events are usually associated with displaying lists and displaying the state of objects.

There are several properties and methods to note when using the Event class.

* first three parameters of the constructor，`type`、`bubbles`and`cancelable`。

   * `type`specify the type of the event, in the case of a “DATE”，`type`event type is“DATE”.The type of event we often use “ADDED”、“COMPLETE” etc。
   * `bubbles`is to specify whether to participate in events stream bubbling phase, about the flow of events, will be in the back of the section.
   * `cancelable`said whether can cancel the default action associated with an event.

* you also need to pay attention to the attribute is a `target`，the goal of this attribute indicates that the event is the sender of the event. Some of the other methods are related to the flow of events, and more on that later.

###  Custom Event

Typically, custom events are written in the game. In the previous section, you wrote a custom event for a "date".

```
class DateEvent extends egret.Event
{
    public static DATE:string = "约会";
    public _year:number = 0;
    public _month:number = 0;
    public _date:number = 0;
    public _where:string = "";
    public _todo:string = "";
    public constructor(type:string, bubbles:boolean=false, cancelable:boolean=false)
    {
        super(type,bubbles,cancelable);
    }
}
```

The custom Event classes `DateEvent`inherited from  `egret.Event`  class. And define a name for  `DATE` attribute, this property for the static properties, type of string.

The above custom events define the data needed for some events, including the date, place, and what to do. When customizing event classes, developers can define event types and event data according to their own needs.
