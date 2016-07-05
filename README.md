# Whats this?

This script is intended for icinga/nagios/icinga2 to check the state of a
systemd service. We check the ServiceState and the Substate.

## install

  apt-get install python3-nagiosplugin python3-gi

## optional features (future)

It is thinkable to check for every systemd service property.

## example code

from gi.repository import GLib, Gio

systemd = Gio.DBusProxy.new_for_bus_sync(Gio.BusType.SYSTEM, 0, None,  'org.freedesktop.systemd1',  '/org/freedesktop/systemd1',  'org.freedesktop.systemd1.Manager', None)

apache2 = Gio.DBusProxy.new_for_bus_sync(Gio.BusType.SYSTEM, 0, None,  'org.freedesktop.systemd1',  systemd.LoadUnit('(s)', 'apache2.service'),  'org.freedesktop.systemd1.Unit', None)

apache2.get_cached_property('ActiveState').unpack()
-> 'active'
apache2.get_cached_property('SubState').unpack()
-> 'running'

apache2.get_cached_property_names()
-> Liste all systemd-properties