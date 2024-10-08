# OpenTransitPredictions
An Elixir service for implementing and testing innovative prediction algorithms on GTFS data

### Whar are Vehicle Arrival Time Predictions?

Before working in public transit, I assumed public transit service always adhered to schedules and those countdown clocks at stations were the objective truth for when a vehicle will arrive. Silly me. In my defense, I grew up riding commuter rail. Now I understand that what we see counting down at a station are vehicle arrival time predictions; an estimate when a transit vehicle, such as a bus, subway, or train will reach upcoming stops on its route (well, trip really). These forecasts provide riders with real-time information about expected arrival times.

### Novel Prediction Algorithms

Researchers and developers have conceived various innovative prediction algorithms. However, testing these algorithms presents several challenges:

1. Access to relevant, real-time transit and schedule data is essential.
2. Data must be fetched, processed, and combined, which requires a robust infrastructure and effort.
3. Hybrid approach may provide better results, but benefit from an architecture the enables a pipeline of prediction operations.
4. There is currently no straightforward, modern platform to easily implement and test new prediction algorithms as modular components.

### Introducing OpenTransitPredictions

OpenTransitPredictions leverages Elixir and public data sources to create a dependable, high-performance platform. This platform allows developers to focus on writing and testing their prediction algorithms using real transit data without needing to build the underlying systems from scratch.

### Project Goal

The project aims to accelerate innovation in public transit prediction by lowering barriers to entry, paving the way for low or no-cost solutions that transit agencies can adopt to provide accurate real-time information to the public.

While reliable arrival time predictions alone won't solve all the challenges facing public transit, they are crucial in building public trust and empowering riders to make informed travel decisions.
