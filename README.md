<img src="./media/Honeywell_Spot_Red+BlackTagline_Right_PNG.png" alt="Honeywell Logo" />


## #FUTURE SHARPER
I am glad that you passed the first stages of the interview process 🎉🥳. Now is the time to show us what you got!

# Problem description:

We currently have a file that must be read everytime, the file gets updated/modified/changed, and the given messages 
must be classified and saved on specific log files. The application must ensure best code practices and performance.
The application also needs to "rollover" the logs once those get 1 MB of data at least.

# Constraints

- Use C++ code compliant with 11 standard (Better known as C++11).
- The file name for watching should be an argument to the application.
  - Don't hardcode the name for the file, we will give you the name on each run of the application.
- New line characters (\n), must be omitted of the logging files.
- You must have the 3 log files:
  - order.log (which must contain logging for order inputs)
  - cancel.log (which must contain logging for cancel inputs)
  - update.log (which must contain logging for update inputs)
- Once one of the logging files gets big enough, those need to be "rollover" and the old file must rename as follows:
  - MMDDYYYY_HHmmSS.[order|cancel|update].log
    - Where:
    - MM = Month
    - DD = Day
    - YYYY = Year
    - HH = Hour
    - mm = minute
    - SS = seconds
- The structure for an order input is as follows:
  - O########_[description{10,35}]--MMDDYYYYHHmmSS
    - Where:
    - O: Is input identifier, in this case O stands for Order, this means the current line is an Order input.
    - ########: Is the place older for the number order, which is 8 digits length, and should be fill with leading 0 if the order number is not big enough, for example:
      - Order number 1 will be 00000001
    - _: It is an underscore to help divide the order number from the description.
    - [description{10,35}]: Is a placeholder for the description of the order, it should contain only alphanumeric characters, and must be 10 characters minimum and 35 maximum.
    - --: Is a double hyphen, that helps to separate the description from the date.
    - MMDDYYYYHHmmSS: Is the date of the order, please read above (rollover name) for a detail description of the fields.
- The structure for an cancel input is as follows:
  - C########--MMDDYYYYHHmmSS
    - Where:
    - C: Is input identifier, in this case C stands for Cancel, this means the current line is Cancel input.
    - ########: Is the place older for the number order, which is 8 digits length, and should be fill with leading 0 if the order number is not big enough, for example:
        - Order number 1 will be 00000001
    - MMDDYYYYHHmmSS: Is the date of the order, please read above (rollover name) for a detail description of the fields.
- The structure for an cancel input is as follows:
  - U########_[description{10,35}]--MMDDYYYYHHmmSS
    - Where:
    - U: Is input identifier, in this case U stands for Update, this means the current line is Update input.
    - ########: Is the place older for the number order, which is 8 digits length, and should be fill with leading 0 if the order number is not big enough, for example:
        - Order number 1 will be 00000001
    - [description{10,35}]: Is a placeholder for the description of the order, it should contain only alphanumeric characters, and must be 10 characters minimum and 35 maximum.
    - _: It is an underscore to help divide the order number from the description.
    - MMDDYYYYHHmmSS: Is the date of the order, please read above (rollover name) for a detail description of the fields.
- Avoid reading all the file from start to end.
- Keep track of the last position the file was read.
- If any of the messages doesn't comply with the previous mentioned structure, then ignore the line and continue reading the file.
- Log all messages to their corresponding log file, for example if you're reading an order message, log the message to order.log file.
- Also log all messages to standard output

## Example of a messages file

> O00000001_this is a test file--01012024000001<br>
> O00000002_this is the second order number--01012024000001<br>
> O12312333_this is another order--01012024000001<br>
> U12312333_this is an update order--01012024000001<br>
> C12312333--01012024000001<br>

# BONUS
The following constraints/functions are not mandatory, but will give additional points.

- Ignore any cancel or update inputs, if the order number is not currently on the order.log file, ignore rolled over log files.
- Remove any message from the order log if you receive a matching cancel order, ignore rolled over log files.
- Update the description of an order on the order.log file if you receive and update input, and the order number matches with one on the order.log file.
- Use CMake as toolchain for the project.
