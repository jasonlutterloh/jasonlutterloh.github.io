---
layout: post
title:  "Upgrading Peloton Metrics's Data Input Method (A Data Transformation Success Story)"
date:   2020-07-25 00:00:00 -0500
author: Jason Lutterloh
---

# Upgrading Peloton Metrics's Data Input Method (A Data Transformation Success Story)

This article explores upgrading the [Peloton Metrics](https://peloton.lutterloh.dev) app to use a CSV upload instead of a pasted JSON response for data input and how a small JavaScript data transformation method made this change simple and easy.

Peloton Metrics allows users to upload their Peloton cycling data in order to visually track their output over time (alongside other metrics). Due to the lack of a public Peloton API with third-party authentication, the app relied on users to login with their member credentials, call the Peloton API directly in the browser (that is used for populating Peloton’s actual application), copy the response payload, and paste that into a form within the app. The app would then parse this and do it’s analysis. It was admittedly a clunky, unfriendly experience.

I had been on the lookout for a better way to manage the data input until a user on Reddit mentioned allowing users to upload their workout data in a CSV format. Peloton provides users with a CSV download of their workout data on their profile so this seemed like a natural fit in the absence of an accessible API. While initially I didn’t like the idea of having to rework my whole app, the CSV upload had the following benefits:

- The CSV isn’t capped by a limit like the API was so it allows for a richer history.
- Downloading (and uploading) a file is much simpler than having users call an API and copy-paste raw JSON.
- Better mobile support. I noticed in testing that some mobile devices don’t support copy-pasting a giant JSON object very well. Mobile devices support downloading (and uploading) a file, however.

Anyways, I finally decided to make the code change and was politely surprised by a data transformation piece I had worked on the week before.

Initially when I built the app, I simply parsed the uploaded JSON and looped through it all a bunch of times to get the data I needed. The data looked something like:

```json
{
  "created_at": 1595608493,
  "device_type": "home_bike_v1",
  "end_time": 1595610353,
  "fitbit_id": null,
  "fitness_discipline": "cycling",
  "has_pedaling_metrics": true,
  "has_leaderboard_metrics": true,
  "id": "1234567890123456789012345689012",
  "is_total_work_personal_record": true,
  "metrics_type": "cycling",
  "name": "Cycling Workout",
  "peloton_id": "1234567890123456789012345689012",
  "platform": "home_bike",
  "start_time": 1595608554,
  "strava_id": "-1",
  "status": "COMPLETE",
  "timezone": "America/Chicago",
  "title": null,
  "total_work": 423607.05,
  "user_id": "1234567890123456789012345689012",
  "workout_type": "class",
  "total_video_watch_time_seconds": 1831,
  "total_video_buffering_seconds": 0,
  "ride": {
    "has_closed_captions": false,
    "content_provider": "peloton",
    "content_format": "video",
    "description": "For a little nostalgia, hop on the Bike to dance and work your way through this 90s themed ride. ",
    "difficulty_rating_avg": 8.3562,
    "difficulty_rating_count": 8392,
    "difficulty_level": "intermediate",
    "duration": 1800,
    "extra_images": [],
    "fitness_discipline": "cycling",
    "fitness_discipline_display_name": "Cycling",
    "has_pedaling_metrics": true,
    "home_peloton_id": "1234567890123456789012345689012",
    "id": "1234567890123456789012345689012",
    "image_url": "https://s3.amazonaws.com/peloton-ride-images/262348706036866fc0f034b4915d70d8fbd9d633/img_1595254742_39bc1ce1c3b04291a75308183b69c45c.png",
    "instructor_id": "1234567890123456789012345689012",
    "is_archived": true,
    "is_closed_caption_shown": false,
    "is_explicit": false,
    "is_live_in_studio_only": false,
    "language": "english",
    "length": 1965,
    "live_stream_id": "1234567890123456789012345689012-live",
    "live_stream_url": null,
    "location": "uk",
    "metrics": ["heart_rate", "cadence", "calories"],
    "original_air_time": 1595249400,
    "overall_rating_avg": 0.992,
    "overall_rating_count": 10110,
    "pedaling_start_offset": 60,
    "pedaling_end_offset": 1860,
    "pedaling_duration": 1800,
    "rating": 0,
    "ride_type_id": "1234567890123456789012345689012",
    "ride_type_ids": ["1234567890123456789012345689012"],
    "sample_vod_stream_url": null,
    "scheduled_start_time": 1595250000,
    "series_id": "1234567890123456789012345689012",
    "sold_out": false,
    "studio_peloton_id": "1234567890123456789012345689012",
    "title": "30 min 90s Ride",
    "total_ratings": 0,
    "total_in_progress_workouts": 24,
    "total_workouts": 16784,
    "vod_stream_url": "https://amd-vod.akamaized.net/vod/bike/07-2020/07202020-ben_alldis-0200pm-bb-1-3f7951f1085b427e825d3b2a0092c2e0/HLS/master.m3u8",
    "vod_stream_id": "1234567890123456789012345689012-vod",
    "class_type_ids": ["1234567890123456789012345689012"],
    "difficulty_estimate": 8.3562,
    "overall_estimate": 0.992
  },
  "created": 1595608493,
  "device_time_created_at": 1595590493,
  "effort_zones": null
}
```

Imagine an array of 100 objects like that! I only needed a small subset of this data but it seemed simple enough to pull out the relevant pieces as I needed them. This worked until I started to deal with same day rides. Long story short, I created my own object to work with and did an initial mapping when initializing the data. The new object looked like:

```json
{
  "date": "2020-07-24",
  "output": 423,
  "title": "30 min Pop Ride",
  "duration": 30,
  "instructor": "Ben Alldis"
}
```

This new object gets passed to a bunch of other analysis methods that extract relevant information, build chart plot points, etc. All of the follow-on data analysis relies on this data structure and field names. It seemed a little unnecessary at the time but it made debugging a lot easier because when I console-logged my object, I only saw relevant data, not the monstrosity that was the original upload.

Enter the CSV Upload feature…

Because I already had a mapped object that all of the data analysis methods used, the CSV code change was as simple as removing the JSON input form, adding an upload input form, parsing the CSV data, looping through its records, and mapping the relevant data to my object. I didn’t have to make mass changes to all of the charting code or other methods. Once I mapped the code, everything just worked (To be fair, I ran into a few hiccups, but not related to this). Anyways, this made me pretty happy and actually felt like all of my years being frustrated with mapping code was worth it. (That’s a rant for another day and much more related to Java than JavaScript.)

Bottom line: If your app consumes any sort of data and then does work using that data, it’s worth considering mapping it to an object that you define. It allows for greater flexibility in the future, especially if that original input changes.
