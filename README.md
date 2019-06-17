# uw-room-hours

**uw-room-hours** is a tool for viewing the weekly course schedules of building rooms at the University of Washington - Seattle. 

It's especially helpful for figuring out when and how long a room is open to use for studying or working on homework. 

> The uw-room-hours tool can be accessed at [https://joshiabhishek.github.io/uw-room-hours/](https://joshiabhishek.github.io/uw-room-hours/) (Updated for Autumn 2019)

## Get & Add Data

The following are the instructions for how to retrieve and add the properly formatted UW Seattle Time Schedule data needed for this tool:

1) Download and install the [**uw-scrapers**](https://github.com/JoshiAbhishek/uw-scrapers) repository code, following its installation steps 

2) Run the following functions in the *uw-scrapers* index.js file to scrape the UW Time Schedule for the given quarter, export the data, parse the exported files, and create a JSON file mapping buildings to rooms to days of the week to courses

```javascript
// Expose the extractCourseInfo function for use in the Puppeteer page instance
await mainPage.exposeFunction("extractCourseInfo", TimeScheduleScraper.extractCourseInfo);

// Scrape and export UW Time Schedule information by major for a quarter
await TimeScheduleScraper.exportCoursesByMajorAndQuarter(mainPage, "SPR2019", function(file_name, data) {
    ExportUtils.exportJSONArray(DATA_EXPORT_BASE_URL + "SPR2019/", file_name, "data", data);
});

// Parse and export the UW Time Schedule data by grouping courses in to arrays mapped from building, room, and day of the week 
TimeScheduleDataParser.exportTimeScheduleDataMappedToLocationFromFolder(DATA_EXPORT_BASE_URL + "SPR2019/", function (data) {
    ExportUtils.exportJSONObject(DATA_EXPORT_BASE_URL, "TSMAP.json", data);
});
```

3) Copy the JSON file's contents and set it equal to the "tsmap" variable in the *uw-room-hours* external javascript file

```javascript
var tsmap = {...}
```

## Terms & License

This software is provided as is, with no guarantees of functionality. You assume full liability for any of your own usage, modification, and distribution of any portion of this software. All such actions relating to this software should comply with relevant laws and policies, including appropriate use of University of Washington services and data as defined by Washington State and the [University of Washington](https://itconnect.uw.edu/work/appropriate-use/).

Licensed under the [GNU](./LICENSE) license. 