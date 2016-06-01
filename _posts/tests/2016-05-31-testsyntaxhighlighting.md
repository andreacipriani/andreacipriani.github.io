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

# objectivec

```objectivec
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

# without any language

```
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

# % objectivec


{% highlight objectivec %}
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
{% endhighlight %}

# % objective-c


{% highlight objective-c %}
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
{% endhighlight %}

# % objc


{% highlight objc %}
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
{% endhighlight %}