---
title: "What is Cron, and why you should know it. "
subtitle: Learn the power of the Cron syntax
date: 2022-06-02T00:19:30.263Z
summary: Learn the power of the Cron syntax
draft: false
type: book
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
weight: 10
---

## What is cron?

Wikipedia states, "the cron command-line utility, also known as cron job, is a job scheduler on Unix-like operating systems. Users who set up and maintain software environments use cron to schedule jobs to run periodically at fixed times, dates, or intervals." [Wikipedia, 2022](https://en.wikipedia.org/wiki/Cron)


### Why is cron useful?

Cron jobs are fairly simple to create and can be run both locally (on Mac and Linux; UNIX based systems) or using a VM instance. A similar service can be used on Windows by utilizing task scheduler.

It is a very usueful utility to automate repetitive tasks as it utilizes the terminal to execute commands based on a set time schedule or interval.

For instance your daily task is to create a pivot table of yesterdays data based on a few dimensions. Rather than doing this manually in excel every single day, creating a Python script that does this for you can be achieved. Using cron this script can then be run in the background using an intuitive command-line utility specifying the interval (i,e once every day at a specific time).

Assuming we have a Python script that reads a folder on our computer, checks for new files, triggers an action when a new file is found (creating a pivot), then saves the pivot to that excel file and moves it to a separate folder. Added functionality can be made such as emailing the excel file, sending an email notification once the script has run and more.

Cron then is set up to run this Pyhton script every morning, and voila! you now automated 10-15 minutes of your day. 

## Declaring a cron job

Using crontab we can declare cron jobs using a special formula consisting of 5 intervals or wildcards ``** ** *`` where each wildcard ``*`` represents minute, hour, day of month, day of week...in this case the wilcard means any so his cron job is running every minute of every hour on every day of every month, seven days a week.

To create a job on a UNIX-like based system (MacOS, Linux) we can use Terminal and type ``crontab -e`` to to enter edit mode:

```bash
# crontab -e

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed

## Example 1:
# Schedule a job at February 2nd, at 9am every year
# .---------------- minute = 0
# |  .------------- hour = 9
# |  |  .---------- day of month = 2nd
# |  |  |  .------- month (1 - 12) = 2nd (February)
# |  |  |  |  .---- day of week (0 - 6) = any value
# |  |  |  |  |
# 0  9  2  2  *  oscar  /usr/local/bin/yearly_backup

## Example 2:
# Schedule a job every Friday, at noon
# .---------------- minute = 0
# |  .------------- hour = 12
# |  |  .---------- day of month = any value
# |  |  |  .------- month (1 - 12) = any value
# |  |  |  |  .---- day of week (0 - 6) = Friday
# |  |  |  |  |
# 0  12 *  *  fri  oscar  /usr/local/bin/yearly_backup


# Empty temp folder every Friday at 5am
0 5 * * 5 rm -rf /tmp/*

# Backup images to Google Drive every night at midnight
0 0 * * * rsync -a ~/Pictures/ ~/Google\ Drive/Pictures/
```

(courtesy of **Corey Schafer**, [Youtube](https://www.youtube.com/watch?v=QZJ1drMQz1A&ab_channel=CoreySchafer), [Github](https://github.com/CoreyMSchafer/code_snippets/blob/master/Cron-Tasks/snippets.txt))


On Windows machines we can use Task Scheduler which does essentially the same thing. Learn more about Windows Task Scheduler [here](https://www.windowscentral.com/how-create-automated-task-using-task-scheduler-windows-10)

If you are familiar with AWS Lambda functions then you can schedule the functions based on the aforementioned cron fromula. 


## Wrapping up

I hope this small introduction gave a overwiew of cron, why and how ir is used, and potenitally why you should know it in case you want to automate tasks.

Useful links:

* Test your cron schedules - [Crontab guru](https://crontab.guru/)
* Learn more about cron - [What is cron and why it is important - CBTnuggets](https://www.cbtnuggets.com/blog/technology/system-admin/cron-what-is-it-and-why-is-it-important)
