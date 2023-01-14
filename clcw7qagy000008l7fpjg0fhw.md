# Redirecting Standard Output using StringIO and Sys module - Python

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673713528804/bc1c6eaa-fe5a-4694-8037-64abb37e63fd.jpeg align="center")

Sometimes, when writing a program there could be a reason not to like writing into a file directly. In programming, one of the practices is to write data into a file because after a program runs finish all the data is lost, to prevent this, programmers write into the file when there is no database or the data is too short or not necessarily for the database.

You can prevent additional code in writing into a file by using the StringIO module available in python, which is in conjunction with the sys module to perform what I called the **complex method** of writing into a file.

The sys module has two methods **stdout** and \_\_**stdout**\_\_(it has more methods}**:**

The formal can easily be redirected to StringIO while the latter holds the standard output for reinitialize when already using the formal and later initialized. what we are saying here is that StringIO captures the print function and writes Its argument into a StringIO object -a file-like object.

The stringIO is present in the io module - input and output module - it should be imported when needed

%[https://gist.github.com/Musoye/b08b1079d6bfa7263a3d34c73e566b74] 

The output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673715888770/f188e448-f676-4a96-bc05-2a0c3c25270d.png align="center")

This is the place we are drawing the veil. Thank you for reading!