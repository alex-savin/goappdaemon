# Go!AppDaemon

![alt text](https://github.com/alex-savin/goappdaemon/blob/master/images/go-appdaemon.png?raw=true)


## Timer Implementation
https://github.com/go-co-op/gocron

## Arguments
https://medium.com/@soheilhy/python-kwargs-and-beyond-in-go-e58f564731aa
https://github.com/soheilhy/args

## Geo Location
https://github.com/tidwall/tile38
https://github.com/consbio/mbtileserver

## Sunrise
https://github.com/kelvins/sunrisesunset

## UPS Monitor
https://github.com/mdlayher/apcupsd
https://github.com/mdlayher/apcupsd_exporter

## WOL
https://github.com/mdlayher/wol

## WireGuard Exporter
https://github.com/mdlayher/wireguard_exporter

## Unifi
https://github.com/mdlayher/unifi
https://github.com/mdlayher/unifi_exporter

## mDNS Tool
https://github.com/ghetzel/mdnstool

## Supported Features (Hass device)
https://community.home-assistant.io/t/how-to-read-interpret-supported-features/114152/9
```
SUPPORT_OPEN = 1
SUPPORT_CLOSE = 2
SUPPORT_SET_POSITION = 4
SUPPORT_STOP = 8
SUPPORT_OPEN_TILT = 16
SUPPORT_CLOSE_TILT = 32
SUPPORT_STOP_TILT = 64
SUPPORT_SET_TILT_POSITION = 128
```

## Features

turn_on(self, entity_id, **kwargs)
self.turn_on("switch.backyard_lights")
self.turn_on("scene.bedroom_on")
self.turn_on("light.office_1", color_name = "green")

turn_off(self, entity_id, **kwargs)
self.turn_off("switch.backyard_lights")
self.turn_off("scene.bedroom_on")

toggle(self, entity_id, **kwargs)
self.toggle("switch.backyard_lights")
self.toggle("light.office_1", color_name = "green")

set_value(self, entity_id, value, **kwargs)
self.set_value("input_number.alarm_hour", 6)

set_textvalue(self, entity_id, value, **kwargs)
self.set_textvalue("input_text.text1", "hello world")

select_option(self, entity_id, option, **kwargs)
self.select_option("input_select.mode", "Day")

notify(self, message, **kwargs)
self.notify("Switching mode to Evening")
self.notify("Switching mode to Evening", title = "Some Subject", name = "smtp")

render_template(self, template, **kwargs)
self.render_template("{{ states('sun.sun') }}")
Returns (str) above_horizon

self.render_template("{{ is_state('sun.sun', 'above_horizon') }}")
Returns (bool) True

self.render_template("{{ states('sensor.outside_temp') }}")
Returns (float) 97.2

get_trackers(self, **kwargs)
get_tracker_details(self, **kwargs)
get_tracker_state(self, entity_id, **kwargs)

anyone_home(self, **kwargs)
everyone_home(self, **kwargs)
noone_home(self, **kwargs)



get_state(self, entity_id=None, attribute=None, default=None, copy=True, **kwargs)
state = self.get_state()
state = self.get_state("switch")
state = self.get_state("light.office_1")
state = self.get_state("light.office_1", attribute="brightness")
tate = self.get_state("light.office_1", attribute="all")

set_state(self, entity_id, **kwargs)
self.set_state("light.office_1", state="off")
self.set_state("light.office_1", state = "on", attributes = {"color_name": "red"})
self.set_state("light.office_1", state="off", namespace ="hass")

listen_state(self, callback, entity=None, **kwargs)
self.handle = self.listen_state(self.my_callback)
self.handle = self.listen_state(self.my_callback, "light")
self.handle = self.listen_state(self.my_callback, "light.office_1")
self.handle = self.listen_state(self.my_callback, "light.office_1", attribute = "all")
self.handle = self.listen_state(self.my_callback, "light.office_1", attribute = "brightness")
self.handle = self.listen_state(self.my_callback, "light.office_1", new = "on")
self.handle = self.listen_state(self.my_callback, "light.office_1", attribute = "brightness", old = "100", new = "200")
self.handle = self.listen_state(self.my_callback, "light.office_1", new = "on", duration = 60)
self.handle = self.listen_state(self.my_callback, "light.office_1", new = "on", duration = 60, immediate = True)

cancel_listen_state(self, handle)
self.cancel_listen_state(self.office_light_handle)

info_listen_state(self, handle)
entity, attribute, kwargs = self.info_listen_state(self.handle)

parse_utc_string(self, utc_string)

get_tz_offset()

convert_utc(utc)

sun_up(self)

sun_down(self)

parse_time(self, time_str, name=None, aware=False)
>>> self.parse_time("17:30:00")
17:30:00
>>> time = self.parse_time("sunrise")
04:33:17
>>> time = self.parse_time("sunset + 00:30:00")
19:18:48
>>> time = self.parse_time("sunrise + 01:00:00")
05:33:17

parse_datetime(self, time_str, name=None, aware=False)
>>> self.parse_datetime("2018-08-09 17:30:00")
2018-08-09 17:30:00
>>> self.parse_datetime("17:30:00")
2019-08-15 17:30:00
>>> self.parse_datetime("sunrise")
2019-08-16 05:33:17
>>> self.parse_datetime("sunset + 00:30:00")
2019-08-16 19:18:48
>>> self.parse_datetime("sunrise + 01:00:00")
2019-08-16 06:33:17

get_now(self)
>>> self.get_now()
2019-08-16 21:17:41.098813+00:00

get_now_ts(self)
>>> self.get_now_ts()
1565990318.728324

now_is_between(self, start_time, end_time, name=None)
>>> if self.now_is_between("17:30:00", "08:00:00"):
>>>     #do something
>>> if self.now_is_between("sunset - 00:45:00", "sunrise + 00:45:00"):
>>>     #do something

sunrise(self, aware=False)
>>> self.sunrise()
2019-08-16 05:33:17

sunset(self, aware=False)
>>> self.sunset()
2019-08-16 19:48:48

cancel_timer(self, handle)
info_timer(self, handle)

run_in(self, callback, delay, **kwargs)
self.handle = self.run_in(self.run_in_c, 10)
self.handle = self.run_in(self.run_in_c, 5, title = "run_in5")

run_once(self, callback, start, **kwargs)
>>> runtime = datetime.time(16, 0, 0)
>>> handle = self.run_once(self.run_once_c, runtime)

>>> handle = self.run_once(self.run_once_c, "10:30:00")

>>> handle = self.run_once(self.run_once_c, "sunset")

>>> handle = self.run_once(self.run_once_c, "sunrise + 01:00:00")

run_at(self, callback, start, **kwargs)
>>> runtime = datetime.time(16, 0, 0)
>>> today = datetime.date.today()
>>> event = datetime.datetime.combine(today, runtime)
>>> handle = self.run_at(self.run_at_c, event)

>>> handle = self.run_at(self.run_at_c, "10:30:00")

>>> handle = self.run_at(self.run_at_c, "2018-12-11 10:30:00")

>>> handle = self.run_at(self.run_at_c, "sunset")

>>> handle = self.run_at(self.run_at_c, "sunrise + 01:00:00")

run_daily(self, callback, start, **kwargs)
>>> runtime = datetime.time(19, 0, 0)
>>> self.run_daily(self.run_daily_c, runtime)

>>> handle = self.run_daily(self.run_daily_c, "10:30:00")

>>> handle = self.run_daily(self.run_daily_c, "sunrise")

>>> handle = self.run_daily(self.run_daily_c, "sunset + 01:00:00")

run_hourly(self, callback, start, **kwargs)
>>> runtime = datetime.time(0, 0, 0)
>>> self.run_hourly(self.run_hourly_c, runtime)

run_minutely(self, callback, start, **kwargs)

>>> time = datetime.time(0, 0, 0)
>>> self.run_minutely(self.run_minutely_c, time)

run_every(self, callback, start, interval, **kwargs)
>>> self.run_every(self.run_every_c, time, 17 * 60)

run_at_sunset(self, callback, **kwargs)
>>> self.run_at_sunset(self.sun, offset = datetime.timedelta(minutes = -45).total_seconds())
>>> self.run_at_sunset(self.sun, offset = 30 * 60)
>>> self.run_at_sunset(self.sun, random_start = -60*60, random_end = 60*60)
>>> self.run_at_sunset(self.sun, random_start = -60*60, random_end = 30*60)

run_at_sunrise(self, callback, **kwargs)
>>> self.run_at_sunrise(self.sun, offset = datetime.timedelta(minutes = -45).total_seconds())
>>> self.run_at_sunrise(self.sun, offset = 30 * 60)
>>> self.run_at_sunrise(self.sun, random_start = -60*60, random_end = 60*60)
>>> self.run_at_sunrise(self.sun, random_start = -60*60, random_end = 30*60)


call_service(self, service, **kwargs)
>>> self.call_service("light/turn_on", entity_id = "light.office_lamp", color_name = "red")
>>> self.call_service("notify/notify", title = "Hello", message = "Hello World")

run_sequence(self, sequence, **kwargs)
handle = self.run_sequence("sequence.front_room_scene")
>>> handle = self.run_sequence([{"light.turn_on": {"entity_id": "light.office_1"}}, {"sleep": 5}, {"light.turn_off":
{"entity_id": "light.office_1"}}])

cancel_sequence(self, handle)

listen_event(self, callback, event=None, **kwargs)
>>> self.listen_event(self.mode_event, "MODE_CHANGE")
>>> self.listen_event(self.generic_event, "zwave.scene_activated", scene_id = 3)
>>> self.listen_event(self.generic_event, "zwave.scene_activated", entity_id = "minimote_31", scene_id = 3)

cancel_listen_event(self, handle)
>>> self.cancel_listen_event(handle)

info_listen_event(self, handle)
>>> service, kwargs = self.info_listen_event(handle)

fire_event(self, event, **kwargs)
>>> self.fire_event("MY_CUSTOM_EVENT", jam="true")
