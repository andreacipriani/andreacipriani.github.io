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

# objc

```objc

NSSortDescriptor *valueDescriptor = [NSSortDescriptor sortDescriptorWithKey:@"description" ascending:YES];

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

# (no language)

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

# Ruby

```ruby

require 'benchmark'
N = 1000
BASIC_LENGTH = 10

5.times do |factor|
  length = BASIC_LENGTH * (10 ** factor)
  puts "_" * 60 + "\nLENGTH: #{length}"

  Benchmark.bm(10, '+= VS <<') do |x|
    concat_report = x.report("+=")  do
      str1 = ""
      str2 = "s" * length
      N.times { str1 += str2 }
    end

    modify_report = x.report("<<")  do
      str1 = "s"
      str2 = "s" * length
      N.times { str1 << str2 }
    end

    [concat_report / modify_report]
  end
end

```

# Swift

```swift

class BankAccount {

    internal private(set) var balance: Int
    private let initialBalance: Int

    init(initialBalance: Int = 80) {
        self.initialBalance = initialBalance
        self.balance = initialBalance
    }

    func resetBalance(){
        self.balance = initialBalance
    }

    func withdraw(amount: Int, completion: @escaping (Result<Int, BankError>) -> Void) {
        if (balance < amount) {
            printWithThread("👎 You can't withdraw \(amount)$ since your balance is \(balance)$")
            completion(.failure(BankError.insufficientBalance))
        }

        printWithThread("👍 Your balance is higher than \(amount)$, preparing withdraw...")
        waitForWindowsXPLatency()
        balance -= amount
        printWithThread("💰 Successfully withdrawn \(amount)$. Your new balance is \(balance)$")
        completion(.success(balance))
    }

    func waitForWindowsXPLatency() {
        sleep(2)
    }
}
```
