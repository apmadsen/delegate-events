[Documentation](/docs/documentation.md) >
 [v0.0](/docs/0.0/version.md) >
  [delegate](/docs/0.0/delegate/module.md) >
   [events](/docs/0.0/delegate/events/module.md) >
    Channel

# Channel[T\<[Event](event.md)\>]

The `Channel` class is the event channel returned by the delegate, and its jobs are handling subscriptions and firing of events.

## Functions

### subscribe(handler: _Callable[[object, T\<[Event](event.md)>], None]_)

The `subscribe` function subscribes a handler function to the channel. The function takes 1 argument:
- handler: `(object, Event) -> None`

#### Example
```python
from delegate.events import Channel

channel = Channel[OnSomethingEvent]()

def handler(sender: object, args: OnSomethingEvent) -> None:
    pass

channel.subscribe(handler)
```


### unsubscribe(handler: _Callable[[object, T\<[Event](event.md)>], None]_)
The `unsubscribe` function unsubscribes a handler function from the channel. The function takes 1 argument:
- handler: `(object, Event) -> None`

```python
from delegate.events import Channel

channel = Channel[OnSomethingEvent]()

def handler(sender: object, args: OnSomethingEvent) -> None:
    pass

channel.subscribe(handler)
channel.unsubscribe(handler)
```

### fire(event: _T\<[Event](event.md)>_, *, ttl: _float | None = 0_) -> _bool_ function
The `fire` function fires the event, invoking all subscribed handlers. The function returns True if event was successfully sent and takes 1 argument:
- event: `Event`

and 1 optional keyword argument:
- ttl: `float | None` the time-to-live (seconds) of the event.

```python
from delegate.events import Channel

channel = Channel[OnSomethingEvent]()

msg_queue: list[Event] = []

def handler(sender: object, event: OnSomethingEvent) -> None:
    msg_queue.append(event)

channel.fire(OnSomethingEvent("Something", "some other thing")) # => False
channel.fire(OnSomethingEvent("Something", "some other thing"), ttl=10) # => False - event stays in queue and will be sent if subcrribed to within 10 seconds though

channel.subscribe(handler)

channel.fire(OnSomethingEvent("Something", "some other thing")) # => True

len(msg_queue) # => 2
```
