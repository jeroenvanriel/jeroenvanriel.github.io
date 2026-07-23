---
layout: post
title:  "Replaying simulations in the browser: streaming and interpolation"
date:   2026-05-02 12:26:00 +0200
categories: traffic
---

I'd like to share another interesting engineering lesson about working with streaming live vehicle motion to a browser. The technique is very similar to how most online video players are implemented.

## Generating vehicle trajectories

- demand specification: trips and routes
- running the simulation and generating FCD data
- custom script to generate FCD data

Our visualization tool needs a set of prerecorded vehicle trajectories; it cannot visualize a running instance of a SUMO simulation (see [Related work](#related-work) for alternatives that support such "live" mode). The most straightforward way is to setup a SUMO simulation and use `sumo-gui` with the [`--fcd-ouput` option](sumo-fcd). Alternatively, your custom script can generate the XML file directly, which was what my thesis supervisor mainly does for his research on autonomous intersections.

An FCD file `fcd.xml` has the following simple structure:

```xml
<fcd-export>
  <timestep time="1.00">
    <vehicle id="veh_1" x="0.000" y="30.000" angle="90.00" />
  </timestep>
  <timestep time="1.25">
    <vehicle id="veh_1" x="0.250" y="30.000" angle="90.00" />
    <vehicle id="veh_2" x="60.000" y="0.000" angle="0.00" />
  </timestep>
  ...
</fcd-export>
```


## The streaming data problem

## Incremental updates: delta packets

Inspired by the sumo-web3d project, and similar to how it is implemented on most websites with some kind of streaming video component, like Youtube, we solve this by only sending incremental updates, or *delta packets*.

## Seeking with snapshots

To support fast seeking without having to rebuild the state from a series of deltas, the backend precomputes a series of complete snapshots at regular intervals. All these snapshots are send to the browser upfront.

The downside of this approach is that the user cannot do a "fine-search" on the timeline.
I decided to solve this as follows. The user can set the timeline slider at any individual frame, but as long as seeking is active, we only render the nearest snapshot. When the user releases the slider, or after some set time has passed, we rebuild the actual state by applying the necessary deltas.

Alternatively, we can use some measure of seke-step-size to choose when to start rebuilding state.
