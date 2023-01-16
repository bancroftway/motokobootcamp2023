#### Question 1: How much is the current memory capacity of a canister?
Answer: By default, canisters use "best-effort" memory allocation when they are created, if we do not specifically ask for a set memory allocation using the command line argument '--memory-allocation'.
However, we can specify the memory allocation by issuing this command, where for example, 12GB memory is being specified for all canisters:
``` 
dfx canister update-settings --memory-allocation 12GB --all
```

#### Question 2: What is the issue with the following code sample?
```
actor {
  let counter : Nat = 0;
  public func increment_counter() : async () {
    counter := counter + 1;
  };
}
```
Answer: Since 'counter' is declared using a 'let' keyword, it is not mutable and cannot be changed. In case mutability is desired, it should be declared using 'var' keyword.

This code will result in compile error:
```
expected mutable assignment target
```

#### Question 3: What is the issue with the following code sample?
```
actor {
  var message : Text = 0;

  public query func change_message(new_message : Text) : async () {
    message := new_message;
    return;
  };
  
  public query func see_message() : async Text {
    return(message);
  };
}
```
Answer: The variable 'message' is declared of type 'Text' but it's value is being set to a Nat, which is not allowed. 