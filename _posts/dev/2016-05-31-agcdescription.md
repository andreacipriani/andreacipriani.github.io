---
layout: post
title: Why I don’t code anymore description methods
modified:
categories: dev
excerpt:
tags: []
image:
  feature:
date: 2016-05-31T17:43:15+02:00
---

# No more description methods

```objective-c
- (NSString*)description
{
	😱 😱 😱 ⌛️⌛️⌛️
}
```

It's boring to write description methods. It's even more boring to keep them updated everytime you modify a class. But great descriptions can improve the quality of your debugging... and save you time!

🎉 Don't worry! It's time to let ```AGCDescription```do the dirty work for you! 🎉

## One step back

What is a description method? 

The description method just *"returns a string that describes the contents of the receiver."* It's like the ```toString()``` method in Java.
Description is a required method of the NSObject protocol, and it's only useful for debugging or logging.

description vs debugDescription

NSLog()
po

Long example:

-(NSString*)description
{
	return [NSString stringWithFormat:@["<%@: %@, %@
}

## AGCDescription

```AGCDescription``` is a category on ```NSObject``` which uses the Objective-C runtime potential to automatically build the description string of any of your classes. And if you gonna change the class, the description will be automatically updated. 

### How to use it - Example

Given a simple class representing a User:

```objective-c

@interface AGCUser : NSObject

- (instancetype)initWithUserId:(NSNumber*)userId username:(NSString*)username password:(NSString*)password userImage:(UIImage*)userImage;

@property (nonatomic, strong) NSNumber* userId;
@property (nonatomic, copy) NSString* username;
@property (nonatomic, copy) NSString* password;
@property (nonatomic, strong) UIImage* userImage;
```

Go the the implementation file, import the category:

```objective-c
#import "NSObject+AGCDescription.h"
```

And delegate ```AGCDescription``` to returns the description strings for you:

```objective-c
- (NSString*)description
{
return [self agc_description];
}

- (NSString*)debugDescription
{
return [self agc_debugDescription];
}
```

You're done. It's easy, no? Let's now print the description of a user to see the result:

```objective-c
AGCUser* agcUser = [[AGCUser alloc] initWithUserId:@(123) username:@"Mick Jagger" password:@"angie123" userImage:[UIImage imageNamed:@"mick.png"]];
NSLog(@"%@",agcUser);
```
This is what will be logged:

```
<AGCUser:
{
userId = 123;
username = Mick Jagger;
password = angie123;
userImage = <UIImage: 0x7faa7a5fb170>, {140, 154};
}>
```

😎😎😎

### Example details

And that's not all! Suppose that after few days you decide that the user should also have an email address property.
You add it into your Class:

```objective-c
@property (nonatomic, copy) NSString* emailAddress;
//...
[agcUser setEmailAddress:@"mick@gmail.com]
```

And you don't need to change your code! The description will be automatically updated - the description is automatically updated also if you remove or rename a property.

```
<AGCUser:
{
userId = 123;
username = Mick Jagger;
password = angie123;
userImage = <UIImage: 0x7faa7a5fb170>, {140, 154};
emailAddress = mick@gmail.com
}>
```

And what if you don't want to log the password of the user? Or you just want to ignore a property (for example the userImage) that is not influent in the description? Use ```agc_descriptionIgnoringPropertiesWithNames``` method:

```objective-c
- (NSString*)description
{
return [self agc_descriptionIgnoringPropertiesWithNames:@[@"password",@"userImage"]];
}
```

And you will protect your secrets 😉
```
<AGCUser:
{
userId = 123;
username = Mick Jagger;
emailAddress = mick@gmail.com
}>
```

### AGCDescription Rules

Let's see how ```AGCDescription``` build the description string:

The format is: 

```
<$ClassName:
{
$firstPropertyName = $firstPropertyValue;
...
$lastPropertyName = $lastPropertyValue;
}>    
```

- Properties are in the some order of your code declaration
- By default these properties are ignored: ```hash, description, debugDescription```

Sometimes property values are too long to be into the description. In that cases a so called *short description* is used, which basically has this format:

```
<$ClassName: $objectAddress>
```

Here are the rules to evaluate the property value:

- If a property is a primitive or a Foundation object with a known short description, print its description as the value 
- If a property is kind of a custom Class, print the short description
- If the property is a collection, print all objects inside the collection
- If one of this object is a custom class, print the short description
- If one of this object is another collection, print the short description of the collection

### Usage

AGCDescripton [is available on Github](https://github.com/andreacipriani/NSObject-AGCDescription) under the MIT license.

### Conclusion

