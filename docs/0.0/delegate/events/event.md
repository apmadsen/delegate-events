[Documentation](/docs/documentation.md) >
 [v0.0](/docs/0.0/version.md) >
  [delegate](/docs/0.0/delegate/module.md) >
   [events](/docs/0.0/delegate/events/module.md) >
    Event

# Event class

The `Event` class is the base class of all events. Events are the classes holding the event information, when an event is fired, thus, when subclassed, should contain properties/fields of the event information.

#### Example
```python
from delegate.events import Event

class OnSomething(Event):
    def __init__(self, what: str, why: str):
        self.what = what
        self.why = why

    def __str__(self):
        return f"{self.what} happened because of {self.why}"

```
