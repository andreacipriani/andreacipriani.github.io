---
layout: post
title: TestSyntaxHighlighting
modified:
categories: tests
excerpt:
tags: []
image:
  feature:
date: 2016-05-31T18:29:30+02:00
---

# objective-c

```objective-c

AGCUser* agcUser = [[AGCUser alloc] initWithUserId:@(123) username:@"Mick Jagger" password:@"angie123" userImage:[UIImage imageNamed:@"mick.png"]];
NSLog(@"%@",agcUser);

- (NSString*)description
{
return [self agc_description];
}

- (NSString*)debugDescription
{
return [self agc_debugDescription];
}

```

# objc

```objc

AGCUser* agcUser = [[AGCUser alloc] initWithUserId:@(123) username:@"Mick Jagger" password:@"angie123" userImage:[UIImage imageNamed:@"mick.png"]];
NSLog(@"%@",agcUser);

- (NSString*)description
{
return [self agc_description];
}

- (NSString*)debugDescription
{
return [self agc_debugDescription];
}

```
