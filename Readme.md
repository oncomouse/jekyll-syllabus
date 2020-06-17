# jekyll-syllabus

This is a stand-alone, Github-Pages-compatible means to generate a course schedule---complete with holidays and any redefined days---from a relatively simple data file.

This inclusion is a standalone spin-off from the more complete [jekyll-course-site](https://github.com/oncomouse/jekyll-course-site), which provides an entire, simple GitHub-Pages compatible syllabus website.

## What This Does

Instead of having to work out a day-by-day schedule grid for a course each semester you teach it, this inclusion allows you to describe course activities in a list (if you had 30 course meetings in a semester, you could describe 30 activities) and to describe the semester in terms of start and end dates, holidays, and any redefined days. From these two collections of data, the inclusion will generate a properly-styled, responsive schedule on your website.

Using software like this allows you to keep one data file describing a course that you can use to easily generate new course websites each semester you teach the course. [Click here to see an example](https://oncomouse.github.io/jekyll-syllabus/).

## How To Use It

There are three files in this repository:

1. `_data/schedule.yml` -- This is the data file that describes your semester
1. `_include/schedule.html` -- This file generates the schedule grid
1. `_sass/schedule.scss` -- This generates the CSS needed to style the grid.

Copy all three files into similar directories (`_data`, `_include`, `_sass`) in your Jekyll repository and then follow the instructions below:

### Adding the schedule grid

