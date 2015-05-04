# HeavenScript
We want to solve the callback-hell that exists in calling to Async function in JavaScript

Hello everyone.

I thought about a solution how to solve the callback hell.

var a=asyncFunction1(parameters,function(err,param1){
  var b=asyncFunction2(parameters,function(err,param2){  
     if (err) console.log(err)
     console.log('here')
  }

I want to create new syntax for calling to async functions.
The new syntax will be as extension to JavaScript (like TypeScript, or CoffeScript but minimalist change to the JS code).
It will be compiled just before Node.jS running the JavaScript.

I have created new GitHub repository. And I want to start developing it. (https://github.com/AminaG/HeavenScript)
I am searching for other developers, who want to join me in this project.
I need help in 2 things:
1. IDE's intellisense. Because I am changing little bit the JavaScript, all IDE's will create warnings. So I need to create new definition files for them (IntelliJ, SublimeText, VS, etc;) Who here know how to do it?
2. Help me with English. My development skills, are much better than English. So for explanations, and create README file, I need help.

//******************************
the new syntax:

a=@asyncFunction1(param1)
err,b=@asyncFunction2(param2)
console.log('now we can access to a,b')

it will be converted to

asyncFunction1(param1,function(err,a){
  if(err) throw err; 
  asyncFunction2(param2,function(err,b){
    console.log('now we can access to param1, param2')
  })
})


//******************************
One More Example:

See how much it is easier and readable to write it in HeavenScript

function theBlock(){
  a=@asyncFunction1(param1)
  err,b=@asyncFunction2(param2)
  console.log('Now we can access a,b,err')
  if (err) {console.log('error in function2'),
  err,c=@asyncFunction3(param3) {
      console.log('Now we can access a,b,c')
  }
  d=@asyncFunction4(param4)
  console.log('Now we can access only to a,b. c is in another scope')
}

(304 characters)

It will be converted to:

asyncFunction1(param1,function(err,a){
  if(err) throw err
  asyncFunction2(param2,function(err,b){
    console.log('Now we can access a,b,err')
    if (err) console.log('error in function2')
      asyncFunction3(param3,function(err,c){
         console.log('Now we can access a,b,c')
      })
      d=asyncFunction4(param4,function(err,d){
          if(err) throw err
           console.log('Now we can access only to a,b. c is in another scope')
     })
    })
})


(391 characters)

What do you think?
