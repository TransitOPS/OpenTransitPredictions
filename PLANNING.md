# Planning

To simplify this application, there are a few standalone components.

### Block Backout Service
When you are running something like this in production, you would have real dispatchers generating data that includes blocks that would read by the prediction service to vehicles could be matched to trips. For testing purposes, one of the MBTA's public feeds will be used to "backout" the base information that would be fed to this service so the service can be built with realistic data inputs and not tied to proprietary formats.

A block might look something like:

```JSON
{
  "block_id": "block_001",
  "vehicle_id": "vehicle_123",
  "block_name": "Morning Peak Service",
  "start_time": "06:00:00",
  "end_time": "10:00:00",
  "trips": ["trip_101", "trip_102"]
}
```

TODO: consider in detail the architecture of this small service, what data it needs and what data format it writes data to.


### GTFS Database File Packing
There are many different ways that this service could obtain the relevant GTFS schedule data it needs. My personal preference would just be to pack some of the MBTA's GTFS files into a Sqlite database format that later, the Elixir service would access via Ecto. Not saying this is the best approach, but GTFS schedule data should fit reasonably well into Sqlite format and this provides a shortcut to some typical GTFS data joining for folks comfortable with SQL.

### Core Service
The Core Service is the main supervised Elixir application.

It will:
- uses environment variables to know what external and local data source to read
- read GTFS schedule data via Ecto from a local Sqlite database
- the results will be parsed and cached in a GenServer
- poll an external GTFS-RT feed for vehicles positions
- call a function-per-vehicle to generate predictions

### Vehicle Function Wrapper
The predicion function encapsulates a set of vehicle specific functions used to generate predictions

It will:
- parse raw vehicle data
- retreive any cached statistics / data pertaining to this vehicle's recent history
- determine the trip of the vehicle using the block, vehicle, location, and current time
- retreive any cached statistics / data pertaining to this trips's recent history
- call any definted prediction algorythms
- store and data for future use
- output a series of new predictions for a range of next stops
