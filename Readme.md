# jekyll-syllabus

This is a stand-alone, Github-Pages-compatible means to generate a course schedule—complete with holidays and any redefined days—from a relatively simple data file.

This inclusion is a standalone spin-off from the more complete [jekyll-course-site](https://github.com/oncomouse/jekyll-course-site), which provides an entire, simple GitHub-Pages compatible syllabus website.

## What This Does

Instead of having to work out a day-by-day schedule grid for a course each semester you teach it, this inclusion allows you to describe course activities in a list (if you had 30 course meetings in a semester, you could describe 30 activities) and to describe the semester in terms of start and end dates, holidays, and any redefined days. From these two collections of data, the inclusion will generate a properly-styled, responsive schedule on your website.

Using software like this allows you to keep one data file describing a course that you can use to easily generate new course websites each semester you teach the course. [Click here to see an example](https://oncomouse.github.io/jekyll-syllabus/).

## How To Use It

There are three files in this repository:

1. `_data/schedule.yml` - This is the data file that describes your semester
1. `_include/schedule.html` - This file generates the schedule grid
1. `_sass/schedule.scss` - This generates the CSS needed to style the grid.

Copy all three files into similar directories (`_data`, `_include`, `_sass`) in your Jekyll repository and then follow the instructions below:

### Editing the schedule

The only file you need to actually edit is `_data/schedule.yml`. It contains all of the information for the schedule grid and has comments explaining how to use it.

#### YAML Contents

The file contains a series of keys, optional ones are marked as such. A couple of notes, dates must be written in the form `YYYY-MM-DD` ('1924-03-21' or '2000-12-14') and you must use two digits for months and days, even if they are less than 10. Days of the week must be written in lower case ('monday' or 'saturday').

The keys are as follows:

* `start` - a string containing the date on which the semester starts.
* `end` - a string containing the date on which the semester ends.
* `meets` - a sequence (list) containing days of the week on which your course meets.
* `classes` - a sequence (list) of strings or blocks that describe the activities of each class in order. Each item in the sequence will be formatted using Markdown.
* `holidays` - *optional* a sequence (list) of mappings (hashes) that define holidays. Each entry has two keys:
	* `date` - a string containing the date of the holiday.
	* `name` - a string containing the name or description of the holiday.
* `redefined` - *optional* a sequence (list) of mappings (hashes) that define redefined days. Each entry has two keys:
	* `date` - a string containing the date being redefined.
	* `is_a` - a day of the week string containing what the redefined day functions as.
* `weeks` - *optional* a mapping (hash) of strings. Each key in the mapping must be a week number represented as a string (`1` becomes `"1"`, etc.) that maps to the title for a given week of instruction.
* `units` - *optional* a sequence (list) of mappings (hashes) that defines information about any units your course is divided into. Each entry has three keys:
	* `start` - a number representing the week of the semester on which a given unit starts.
	* `title` - *optional* a string providing a unit title.
	* `description` - *optional* a string or block containing a description of the unit. Will be formatted as Markdown.

Read more about YAML here: [YAML](https://yaml.org/)

### Adding the schedule grid

The schedule can be included anywhere in a `.md` or a `.html` file anywhere in your Jekyll repo. For instance:

~~~liquid
{% include schedule.html %}
~~~

#### Using Multiple Schedules on the Same Site

You can also use multiple schedule files on the same site by passing a `schedule` argument to the include tag. For instance, say you had a syllabus stored in `_data/engl210fall2020` instead of the default `_data/schedule.yml`. You could include that schedule in your site using:

~~~liquid
{% include schedule.html schedule="engl210fall2020" %}
~~~

For more on including files, [see the Jekyll documentation on the topic](https://jekyllrb.com/docs/includes/)

### Adding the styles

You must be using SASS/SCSS on your site for this to work, but you can include the styles in your main SCSS file by adding the following anywhere in that file:

~~~scss
@import "schedule";
~~~

If you are using CSS only, you can include the following CSS in your site:

~~~css
.schedule__date,.schedule__no-class,.schedule__redefined-day{font-weight:700}
.schedule__no-class-name,.schedule__redefined-class{font-style:italic}
.schedule:before,.schedule:after{content:"";display:table;clear:both}
.schedule__meeting,.schedule__week{float:left;padding-left:10px;padding-right:10px}
.schedule__week{width:100%}
.schedule__meeting--dummy{display:none}
@media (min-width: 768px){
	.schedule__meeting--dummy{display:block}
	.schedule--1-per-week .schedule__meeting{width:100%}
	.schedule--2-per-week .schedule__meeting{width:50%}
	.schedule--3-per-week .schedule__meeting{width:33.3333333333%}
	.schedule--4-per-week .schedule__meeting{width:25%}
	.schedule--5-per-week .schedule__meeting{width:20%}
	.schedule--6-per-week .schedule__meeting{width:16.6666666667%}
	.schedule--7-per-week .schedule__meeting{width:14.2857142857%}
}
~~~

To read more about SASS/SCCS in Jekyll, [see the Jekyll documentation on the topic](https://jekyllrb.com/docs/assets/#sassscss).
