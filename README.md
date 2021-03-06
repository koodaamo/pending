# Pending events awaitable for asyncio

Instantiate a Pending awaitable, register events scheduled to be returned after
a given number of seconds, and then await. 

Once the first one (with smallest scheduling delay) is returned, re-await to get
the next one, and so on. Optionally cancel or postpone (reschedule) scheduled events.

Example of use:

```python
>>> import asyncio
>>> from pending import Pending
>>> events = Pending()
>>> events.schedule("second", 10)
>>> events.schedule("first", 9)
>>> async def main():
...    for i in len(events):
...       evt = await events
...       print(evt)
...
>>> asyncio.run(main())
first
second
```

Note: the registered "event" can be any hashable object.
