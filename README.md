<h1>Preface</h1>
The purpose of this article is to spread awareness of script utility engines and educating new developers on how to properly deal with malicious users that take use of tools such as Synapse X. I've taken it as the main example due to its popularity, but by no means does it mean that Synapse is the only threatening injector. This is NOT a sequel to
<a href="https://devforum.roblox.com/t/exploiting-explained/170977">Exploiting Explained</a>, it has an entirely different premise. Please give it a chance.

<h1>Abstract</h1>
Roblox is entering the mainstream media in a bigger way than ever. It is the second largest platform for kids under 13, valued at over 30 billion dollars. However, exploiters are not getting fewer. The increasing number of exploits being spread around has incentivized developers to take a harsher and a more innovative approach on security against popular script utility softwares such as Synapse X.

You should always design your game around the gameplay instead of the security. It is an endless battle and, there will always be malicious exploiters crawling around and it is near impossible to write code that will patch every exploit of the past, present and future. Wanting to prevent injections from Synapse is understandable, but there's not much you can do against it. Surrender the fight on the client and work on authorising everything on the server. 

<h1>What is Synapse X</h1>
Exploiters take use of tools such as Synapse X's decompiler to read client scripts, which is how they find vulnerabilities in our code and exploit them. Pretty much fair game. Synapse X unlike other script utility engines runs at higher "indentities" than normal scripts does. Which gives access to restricted functions that allows for extended functionality and supervision of other normal scripts. 

<h1>The combat</h1>
Few developers combatted the injection of Synapse X by reading malicious clients' memory usages and kicking them on spikes. While it gave false-positives, it did work for a while, until the implementation of auto-attach came long. Which is a boolean that the exploiter can enable to directly inject as soon as the game starts for them.

Synapse X runs on the principle that Lua uses metatables. Metatables allows for vastly more advanced logic to be applied onto the regular tables (**cough** shitty hashtables). They're used everywhere, whether you were conscious of it or not. <img src = "https://doy2mn9upadnk.cloudfront.net/uploads/default/original/4X/e/8/e/e8e2d74c97e46986834260f410f695e8f86eafac.png">

Simply indexing the character of the client calls on metamethods (...exclusive functions of metatables) 3 times. Synapse X takes advantage of this fact, it allows exploiters to hook onto metatables and run implicit functions that you never intended for. Remote Events are objects, and of course, they have metatables. So everytime you call :FireServer, you implicitly invoke the namecall metamethod which exploiters can easily hook onto and change all the arguments, or preventing them from being sent at all.
<img src = "https://doy2mn9upadnk.cloudfront.net/uploads/default/original/4X/2/2/b/22b10099823e633399ee8445f38bace1d5bf26f9.png">

Which is why you will constantly hear experienced developers nag you about NEVER trusting the client! On the topic of measures on the client, the reason why you should never have anti-cheat on the client is 1. they can be disabled, modified and/or bypassed. Using aforementioned knowledge, they can simply do this:

<img src = "https://doy2mn9upadnk.cloudfront.net/uploads/default/original/4X/7/0/4/7041d9d725bd488a6639bb2ac858dd93667bc18c.png>

This is obviously extremely problematic and up until recently, there was a pretty profound way to combat this. It was via checking whether there was any metatable tampering at all.

<img src = "https://doy2mn9upadnk.cloudfront.net/uploads/default/original/4X/a/f/c/afc958b2135b9c8b1e7b28f8c471d0ec2ada84d4.png">
However, recently Synapse X has bypassed this by replacing the function with a new cclosure function (C function). In a running example of an "anti-kick" script, it would look like this: <img src = "https://doy2mn9upadnk.cloudfront.net/uploads/default/original/4X/c/f/0/cf0dc0f06a8af088a46fa5bac50d7e213f303e76.png">

This signifies how important it is to handle this type of logic on the server. 

<h1>Conclusion</h1>
Exploits makes the gameplay's atmosphere very dreadful for some players, so it is understandable that you would like to do anything to prevent it. However, it is important to know that it is impossible to end exploiting. While exploiters are large in numbers, they make up a small portion of your playerbase, and it is much more important to prioritise them. There's not much you as an individual can do. There are extreme geniuses out there that has made anti-cheats that predicts the clients' next interactions and runs sanity checks on that but realistically implementing those are expensive and you should NOT focus on them ever. Code smart, secure your remotes and patch by exploit.
