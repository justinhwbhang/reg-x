# Regular Expression Tutorial

This tutorial serves as a basic reference guide for those learning regular expressions. It focuses on a specific regex used to search for email addresses and examines the different parts of the regex. By the end of the tutorial, the reader will understand the concept of regular expressions, when they should be used, and how to use the different components.

## Summary

A regular expression, or "regex", is a statement that defines a specific pattern of characters that can be searched for in a file or directory. The purpose of the regex is to find and return a match for a sequence of characters. The regex can specify the type, number and order of characters to be matched.

## Table of Contents

- [Regular Expression Tutorial](#regular-expression-tutorial)
  - [Summary](#summary)
  - [Table of Contents](#table-of-contents)
  - [Regex for an email address](#regex-for-an-email-address)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [Character Classes](#character-classes)
    - [Grouping and Capturing](#grouping-and-capturing)
  - [About the Author](#about-the-author)

## Regex for an email address
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

- An email address is composed of three main parts: the "username", the "domain name" separated by an '@' symbol, and the "domain extension" following a '.'. The final format appears as: (username)@(domain name).(domain extension). These three components will be discussed in detail throughout the tutorial.


## Regex Components

### Anchors

- Description: <br>
  > Anchors are used to match a character or phrase at the beginning or end of a line. The end of a line is defined as a sequence of characters that is ended by a return. The ^ character is used to indicate the start of a line and the $ character is used to indicate the end of a line in regular expressions.
 
- Use in our email address regex:
  > Our email address regex utilizes both the `^` "start-of-line" anchor and the `$` "end-of-line" anchor. These anchors appear at the start and end of our expression like this: `/^(regex)$/` This means that if a string is to be matched by our regex, it must be located at both the start and the end of a line. In other words, any email address that's matched by our regex must be on it's own line.

- Example:
  > Given the phrase below, let's say we want to use the `^` and `$` anchors to match a character of any kind at the beginning and end of the line. In our regex, we'll use the `.` period character to match any character at the start or end of the line.

  Phrase: 
  ```
  "I wanted to eat, so I ate a cheeseburger at McDonald's"
  ```

  <br>

  - Demo: Using the `^` "start-of-line" anchor

    Regex: 
    
    ``` 
    /^./
    ```

    Match: <br>
    > ![Start (single line)](https://user-images.githubusercontent.com/87861603/143735449-e50525b3-b05b-430d-968d-60ace53dd30b.png)
    
    Explanation: <br>
    > The regex `/^./` is basically saying, "Find an instance of `.` any character located at the `^` beginning of a line." The "I" is matched since it's a character and it's located at the beginning of a line.

  <br>

  - Demo: Using the `$` "end-of-line" anchor

    Regex: 
    
    ``` 
    /.$/
    ```

    Match: <br>
    > ![end (single line)](https://user-images.githubusercontent.com/87861603/143735469-2f10f7f3-f31f-4de0-a210-18cb8ec87213.png)
    
    Explanation: <br>
    > The regex `/.$/` is basically saying, "Find an instance of `.` any character located at the `$` end of a line." The "s" is matched since it's a character and it's located at the end of a line.

<br>

### Quantifiers

- Description: <br>
  > Quantifiers are used to return a match for a specific number of a characters. Using quantifiers, we can be very specific in how many instances a certain character should exist in a given criteria, or we can be very broad. Either way, quantifiers are very important in finding the characters or phrase we're searching for.

- All regex quantifiers:

  ```
    *     -> 0 or More
    +     -> 1 or More
    ?     -> 0 or One
    {x}   -> Exact Number
    {x,y} -> Min and Max range of numbers
  ```

- Use of quantifiers in our email address regex:

  > Our email address regex uses the + and {x,y} quantifiers to match the       user-name, domain-name, and domain-extension parts.
    The + character at the end of the character class signifies that the regex will match any character in the class if it appears one or more times.
    For example, in the user-name part, we see [a-z0-9_\.-]+ which means the regex will match any character in the class if it appears one or more times.
    Similarly, in the domain-name part, we see [\da-z\.-]+ the + character is used in the same way as in the user-name part.
    In the domain-extension part, we see [a-z\.]{2,6}, the {2,6} signifies that the regex will match any character in the class if it appears between 2-6 times.
    All three criteria must be met for the email address to be matched by the regex.
  
- Example:
  > Let's take a closer look at how quantifiers work but using all the different quantifier characters to return specific matches from the phrase below.

  Phrase:
  ```
  I am very veryy veryyy veryyyy hungry
  ```

  <br>

  - Demo #1) Using the `*` "0 or more" quantifier: <br>
    
    Regex: 
    
    ``` 
    /very */
    ```

    Match: <br>
    ![*](https://user-images.githubusercontent.com/87861603/144788009-0d86371b-b88e-4274-9b8d-314ae096892b.png)
    
    Explanation: <br>
    > The regex `/very */` is basically saying, "Find all instances of 'very' that are followed by 0 or more " " space characters."

  <br>

  - Demo #2) Using the `+` "1 or more" quantifier: <br>

    Regex: 
    
    ``` 
    /very +/
    ```

    Match: <br>
    ![+](https://user-images.githubusercontent.com/87861603/144787988-2ab92b5d-cbcb-42b3-ace6-1812f70aa4f5.png)
    
    Explanation: <br>
    > The regex `/very +/` is basically saying, "Find all instances of 'very' that are followed by one or more " " space characters."

  <br>

  - Demo #3) Using the `?` "0 or one" quantifier: <br>

    Regex: 
    
    ``` 
    /very?/
    ```

    Match: <br>
    ![?](https://user-images.githubusercontent.com/87861603/144788034-500446ad-a2d5-4ca8-bcc9-03bf2901eec4.png)
    
    Explanation: <br>
    > The regex `/very?/` is basically saying, "Find all instances of 'ver' that are followed by 0 or 1 "y" characters."

### Character Classes

- Description <br>
  > Character classes are used to find matches of a specific character set and are invoked with the `[]` brackets. You can also join multiple character sets together by simply adding the next set immediately after the previous set.

- Use in our email address regex:
  > Our email address regex utilizes character classes in the user-name, domain-name and domain-extension parts. 
  In the user-name part, we see `[a-z0-9_\.-]`. This is saying the character in the user-name position of the email address must be either a `a-z` lowercase letter, a `0-9` numeric character from 0-9, an `_` underscore, a `\.` period or a `-` dash.
  In the domain-name part, we see `[\da-z\.-]`. This is saying the character in the domain-name position of the email address must be either a `\d` digit, a `a-z` lowercase letter, a `\.` period or a `-` dash.
  In the domain-extension part, we see `[a-z\.]`. This is saying the character in the user-name position of the email address must be either a `a-z` lowercase letter or a `\.` period,

- Example:
  > Given the list of user data below, let's say we only wanted to match and return the phone numbers of each user. We could write a regex to do this for us. All of the users have input their phone numbers in different formats and including different symbols, but we can utilize the `[]` character classes to include different sets of characters in our search and match all of the phone numbers. 

  Data:

  ```
  Sally Johnson:
  Email: sally.johnson@gmail.com
  Phone: 1231231234

  Robert Tyler:
  Email: bobT@aol.com
  Phone: 234-234-2345

  Carter Gonzales
  Email: c-gonzales8765@verizon.net
  Phone: (345)-345-3456

  Sue Parker
  Email: sue.p@sbcglobal.net
  Phone: 1-(456)-456-4567
  ```

  Regex:
  ```
  /(1-)?([0-9()]{3,5})-?([0-9]{3})-?([0-9]{4})/
  ```
  Match: <br>
  ![User data](https://user-images.githubusercontent.com/87861603/144983188-e673d433-2f34-4927-b8e4-fcf91a45ea97.png)  

  Explanation:
  > Here, we utilized the `[]` character classes in all 3 parts of the phone number format. 
  For the area code, we have `[0-9()]` which will return a match for any number from 0-9 and also any `()` parentheses characters.
  For the middle part, we have `[0-9]` which will return a match for any number from 0-9.
  And finally for the last 4 digits, we have `[0-9]` which will once again return a match for any number from 0-9.
  Together with quantifiers and grouping, the character classes we used has made it possible for us to match all the phone numbers in our user data despite their varying format.

<br>

### Grouping and Capturing

- Description: <br>
  > Capture groups are used to separate a series of regex criteria so they can be defined and saved in memory as their own group. These capture groups are defined with the `()` parentheses. Once defined and saved, these groups can be referenced in a find or replace operation or for backreferencing.

- Use in our email address regex: <br>
  > Our email address regex utilizes capture groups in the user-name, domain-name and domain-extension parts.
  In the user-name part, we see `([a-z0-9_\.-]+)`. This is saying that this capture group must have `+` one or more characters that could be a `a-z` lowercase letter, a `0-9` numeric character from 0-9, an `_` underscore, a `\.` period or a `-` dash. 
  In the domain-name part, we see `([\da-z\.-]+)`. This is saying that this capture group must have `+` one or more characters that could be a `\d` digit, a `a-z` lowercase letter, a `\.` period or a `-` dash.
  In the domain-extension part, we see `([a-z\.]{2,6})`. This is saying that this capture group must have `{2,6}` 2-6 characters that could be a `a-z` lowercase letter or a `\.` period

- Example:
  > Let's say we've created an application that gives us the current weather and a 24 hour forecast for the city we select. Since we're not a weather service, we're using an api that gives us our desired information when we request it. Occasionally there's an error that occurs when our application attempts to connect with the api. It gives us a message like the one below with a lot of different information about the error all grouped together into one long string. We can use a regular expression that matches that error message and separates the different bits of information into groups so we can quickly and easily extract the information we want.

  Error message:

  ```
  2021-11-06; 04:01.890; ERROR: The resource you requested was not found; USER: R+H/L)%%R7^V6IN68'2&//1;XB4T'_;
  ```

  Regex:

  ```
  /^(\d{4}-\d{2}-\d{2}); (\d{2}:\d{2}.\d{3}); (ERROR: .+); (USER: [A-Z\d\+/)%^'&;_]+);$/
  ```

  Explanation:
  > With this regex, all the different bits of information in this error message are now organized into capture groups.

  ```
    Group 0 (Entire message)  -> 2021-11-06; 04:01.890; ERROR: The resource you requested was not found; USER: R+H/L)%%R7^V6IN68'2&//1;XB4T'_;
    Group 1 (Date)            -> 2021-11-06
    Group 2 (Time)            -> 04:01.890
    Group 3 (Error message)   -> ERROR: The resource you requested was not found
    Group 4 (User ID)         -> USER: R+H/L)%%R7^V6IN68'2&//1;XB4T'_
  ```

  > Now that we have all the information separated, we can write a function that returns only the groups of information we want. We do this by referencing the group with the `$` dollar sign followed by the group number. For instance, if we wanted to only display the the Date and Error message, we can write a function that references those groups as `$1` and `$3`.

<br>
