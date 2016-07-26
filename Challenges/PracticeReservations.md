# Overview

For both practice tables and practice judging rooms 

# Practice Reservations elements

In the most simpelest form a volunteer 'manages' a flipover with slots and allows teams to write their name in it. He will make sure teams only take one table in a time slot and maybe limit the maximum reservations per team per day.

The application should provide three interfaces:
1. Setup interface
2. Admin interface
3. Team interface

## Setup interface
In this interface the admin can setup the event specific information. The number of tables or rooms available, the timeslot length and start times. Take note that blocks of slots can start at different times (i.e. not continues). The admin should also have the option to block slots or reserver them for tournament purposes. The admin should have to option to set global settings for the maximum of reservations, to allow for multiple reservations in a time slot and the option to verify reservations. This means that reservations can be approved before becomming difinitive.

## Admin interface
This is the daily interface where an admin can check if and which teams made the reservation and check for attendence.

## Team interface
This is the interface where a team can claim/release slots and view empty slots. There should be somekind of team verification (teamnumber and the name of the coach as password?) Don't make it to difficult, since fair play should be top of mind.

# API
This application should interface with the teamlist.

A more advanced enhancement is the ability to send updates and reminders to the [team app](https://github.com/FirstLegoLeague/Coordination/blob/master/Challenges/TeamApp.md)

