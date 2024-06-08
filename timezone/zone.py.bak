import logging
import os
import gi

import subprocess

gi.require_version("Gtk", "3.0")
from gi.repository import Gtk, Pango

from ks_includes.screen_panel import ScreenPanel

def create_panel(*args):
    return ZonePanel(*args)

class ZonePanel(ScreenPanel):
    def __init__(self, screen, title):
        super().__init__(screen, title)

        self._screen = screen

        self.continent_value = self._config.get_config()['main'].get('timezone', None)
        self.city_value = self._config.get_config()['main'].get('timezone_city', None)

        self._screen.base_panel.show_back(False)
        self._screen.base_panel.show_estop(False)
        self._screen.base_panel.show_macro_shortcut(False)

        self.continent_list = [
            {'name': 'UTC', 'value': 'UTC'},
            {'name': 'America', 'value': 'America'}, 
            {'name': 'Asia', 'value': 'Asia'}, 
            {'name': 'Atlantic', 'value': 'Atlantic'}, 
            {'name': 'Australia', 'value': 'Australia'}, 
            {'name': 'Europe', 'value': 'Europe'}
        ]

        continent_title = _("Setup Timezone")
        self.continent_label = Gtk.Label()
        self.continent_label.set_hexpand(True)
        self.continent_label.set_halign(Gtk.Align.CENTER)
        self.continent_label.set_markup("<span font='DejaVu Sans-bold 33'>{}</span>".format(continent_title))
        
        self.continent_title_box = Gtk.Box()
        self.continent_title_box.set_size_request(480, 80)
        self.continent_title_box.set_valign(Gtk.Align.END)
        self.continent_title_box.add(self.continent_label)

        self.content.add(self.continent_title_box)

        self.continent_menu = Gtk.ComboBoxText()
        for key, value in enumerate(self.continent_list):
            self.continent_menu.append(value['value'], _(value['name']))
            if value['value'] == self._config.get_config()['main'].get('timezone', 'UTC'):
                self.continent_menu.set_active(key)
                self.init_continents_citys(value['value'])

        self.continent_menu.connect("changed", self.on_cities_changes)
        self.continent_menu.set_entry_text_column(0)
        self.continent_menu.set_size_request(440, 80)
        self.continent_menu.set_halign(Gtk.Align.CENTER)
        self.continent_menu.set_valign(Gtk.Align.START)
        self.continent_box = Gtk.Box()
        self.continent_box.set_halign(Gtk.Align.CENTER)
        self.continent_box.pack_start(self.continent_menu, False, False, 15)
        self.continent_box.set_size_request(480, 190)
        self.continent_box.add(self.continent_menu)

        self.content.add(self.continent_box)

        # City
        city_title = _("The City or AREA")
        self.city_label = Gtk.Label()
        self.city_label.set_hexpand(True)
        self.city_label.set_halign(Gtk.Align.CENTER)
        self.city_label.set_markup("<span font='DejaVu Sans-bold 33'>{}</span>".format(city_title))
        
        self.city_title_box = Gtk.Box()
        self.city_title_box.set_size_request(480, 80)
        self.city_title_box.set_valign(Gtk.Align.END)
        self.city_title_box.add(self.city_label)

        self.content.add(self.city_title_box)

        self.city_menu = Gtk.ComboBoxText()

        for key, value in enumerate(self.timezones_citys):
            self.city_menu.append(value['value'], _(value['name']))
            if value['value'] == self._config.get_config()['main'].get('timezone_city', 'UTC'):
                self.city_menu.set_active(key)

        self.city_menu.connect("changed", self.on_select_timezone)

        self.city_menu.set_entry_text_column(0)
        self.city_menu.set_size_request(440, 80)
        self.city_menu.set_halign(Gtk.Align.CENTER)
        self.city_menu.set_wrap_width(3)
        self.city_menu.set_valign(Gtk.Align.START)
        self.city_box = Gtk.Box()
        self.city_box.set_halign(Gtk.Align.CENTER)
        self.city_box.pack_start(self.city_menu, False, False, 15)
        self.city_box.set_size_request(480, 190)
        self.city_box.add(self.city_menu)

        self.content.add(self.city_box)

        self.finish_btn = self._gtk.Button("complete",_("Finish"), f"color1")
        self.finish_btn.set_size_request(480, 80)
        self.finish_btn.set_halign(Gtk.Align.CENTER)
        self.finish_btn.set_valign(Gtk.Align.CENTER)
        self.finish_btn.connect("clicked", self.on_finish_btn)

        self.content.add(self.finish_btn)



    def init_continents_citys(self, continent):
        self.continent = continent
        continents_citys = {
                                "America": [{
                                    "name": "New_York",
                                    "value": "New_York"
                                }, {
                                    "name": "Toronto",
                                    "value": "Toronto"
                                }],
                                "Asia": [{
                                    "name": "Shanghai",
                                    "value": "Shanghai"
                                }, {
                                    "name": "Singapore",
                                    "value": "Singapore"
                                }, {
                                    "name": "Nicosia",
                                    "value": "Nicosia"
                                }],
                                "Atlantic": [{
                                    "name": "Azores",
                                    "value": "Azores"
                                }, {
                                    "name": "Bermuda",
                                    "value": "Bermuda"
                                }, {
                                    "name": "Cape_Verde",
                                    "value": "Cape_Verde"
                                }, {
                                    "name": "Faroe",
                                    "value": "Faroe"
                                }, {
                                    "name": "Madeira",
                                    "value": "Madeira"
                                }, {
                                    "name": "Reykjavik",
                                    "value": "Reykjavik"
                                }, {
                                    "name": "South_Georgia",
                                    "value": "South_Georgia"
                                }, {
                                    "name": "St_Helena",
                                    "value": "St_Helena"
                                }, {
                                    "name": "Stanley",
                                    "value": "Stanley"
                                }],
                                "Australia": [{
                                    "name": "Adelaide",
                                    "value": "Adelaide"
                                }, {
                                    "name": "Brisbane",
                                    "value": "Brisbane"
                                }, {
                                    "name": "Broken_Hill",
                                    "value": "Broken_Hill"
                                }, {
                                    "name": "Darwin",
                                    "value": "Darwin"
                                }, {
                                    "name": "Eucla",
                                    "value": "Eucla"
                                }, {
                                    "name": "Hobart",
                                    "value": "Hobart"
                                }, {
                                    "name": "Lindeman",
                                    "value": "Lindeman"
                                }, {
                                    "name": "Lord_Howe",
                                    "value": "Lord_Howe"
                                }, {
                                    "name": "Melbourne",
                                    "value": "Melbourne"
                                }, {
                                    "name": "Perth",
                                    "value": "Perth"
                                }, {
                                    "name": "Sydney",
                                    "value": "Sydney"
                                }],
                                "Europe": [{
                                    "name": "Amsterdam",
                                    "value": "Amsterdam"
                                }, {
                                    "name": "Athens",
                                    "value": "Athens"
                                }, {
                                    "name": "Berlin",
                                    "value": "Berlin"
                                }, {
                                    "name": "Bratislava",
                                    "value": "Bratislava"
                                }, {
                                    "name": "Brussels",
                                    "value": "Brussels"
                                }, {
                                    "name": "Bucharest",
                                    "value": "Bucharest"
                                }, {
                                    "name": "Budapest",
                                    "value": "Budapest"
                                }, {
                                    "name": "Copenhagen",
                                    "value": "Copenhagen"
                                }, {
                                    "name": "Dublin",
                                    "value": "Dublin"
                                }, {
                                    "name": "Helsinki",
                                    "value": "Helsinki"
                                }, {
                                    "name": "Kiev",
                                    "value": "Kiev"
                                }, {
                                    "name": "Lisbon",
                                    "value": "Lisbon"
                                }, {
                                    "name": "Ljubljana",
                                    "value": "Ljubljana"
                                }, {
                                    "name": "London",
                                    "value": "London"
                                }, {
                                    "name": "Luxembourg",
                                    "value": "Luxembourg"
                                }, {
                                    "name": "Madrid",
                                    "value": "Madrid"
                                }, {
                                    "name": "Malta",
                                    "value": "Malta"
                                }, {
                                    "name": "Oslo",
                                    "value": "Oslo"
                                }, {
                                    "name": "Paris",
                                    "value": "Paris"
                                }, {
                                    "name": "Prague",
                                    "value": "Prague"
                                }, {
                                    "name": "Riga",
                                    "value": "Riga"
                                }, {
                                    "name": "Rome",
                                    "value": "Rome"
                                }, {
                                    "name": "Sofia",
                                    "value": "Sofia"
                                }, {
                                    "name": "Stockholm",
                                    "value": "Stockholm"
                                }, {
                                    "name": "Vienna",
                                    "value": "Vienna"
                                }, {
                                    "name": "Vilnius",
                                    "value": "Vilnius"
                                }, {
                                    "name": "Warsaw",
                                    "value": "Warsaw"
                                }, {
                                    "name": "Zagreb",
                                    "value": "Zagreb"
                                }],
                                "UTC": [{
                                    "name": "UTC",
                                    "value": "UTC"
                                }]
                            }
        self.timezones_citys = continents_citys[continent]

    def on_cities_changes(self, widget):
        self.init_continents_citys(widget.get_active_id())
        self.city_value = None
        self.city_menu.remove_all()
        for key, value in enumerate(self.timezones_citys):
            self.city_menu.append(value['value'], _(value['name']))
            if value['value'] == self._config.get_config()['main'].get('timezone_city', 'UTC'):
                self.city_menu.set_active(key)
                self.city_value = value['value']

    def on_select_timezone(self, widget):
        self.continent_value = self.continent_menu.get_active_id()
        self.city_value = self.city_menu.get_active_id()

    def on_finish_btn(self, widget):
        if self.continent_value == None or self.city_value == None:
            return
        self._screen._config.set("main", "timezone", self.continent_value)
        self._screen._config.set("main", "timezone_city", self.city_value)
        self._screen._config.save_user_config_options()
        if self.continent_value == "UTC":
            target = "UTC"
        else:
            target = self.continent_value + "/" + self.city_value
        with open('/home/mks/target_timezone.txt', 'w') as f:
            f.write(target)
        os.system("systemctl restart KlipperScreen.service")

