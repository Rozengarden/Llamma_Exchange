# [WIP] Llama_Exchange_Stategy

___

A basic understanding of defi is advised.
___

## Abstract

NFTStrategies from Tokenwork have been picking up in popularity recently (with my writing speed thee
 fad might be dead by the time you read this line). After a brief introduction to the subject we will discuss the specificity of The Llamas collection on how they can impact the working of of the original design. This will be followed by the introduction of alternative designs that makes use of those specificity, how different token model could enhance it and the possible upsides and downsides. Finaly a section will be dedicated to the implementation details and possible hurdles.
___

## Introduction

### What's the Strategy ?

If you are familiar with Bitcoin you might have heard of MicroStrategy the company owned by Michael Sailor which is accumulating bitcoin en masse. This is done mainly by debt backed by convertible debt (I will not pretend I know what it means). As the share price went up a lot other company followed suite, using diverse means (debt, convertible or not, spare cash, etc) to acquire crypto (mainly bitcoin, ETH for some, and sometime SOL) and add it to their treasury. Those company are commonly refered  as Digital Asset Treasury (abreviated DAT), but many adopted the word “Strategy" as part of their branding



### NFTStrategy

NFTStrategy from TokenWork work as follow:

1. Take a 10% fee on the token/eth swap on a specific uniV4 pool
2. Use those fee to buy an nft from the collection
3. Relist the nft at ×1.2 of the buy price
4. When sold use this moni to buy-back & burn the token from step one, this is the incentives to fuel the speculation on the token, generating swap fee, thus sustaining the flywhell.

### The Llamas

Llamas is an NFT collection with 1111 token, but unlike most collection the money raised trough the sell in an auction have been used to create a treasury, mainly centered around the curve ecosystem, this treasury has been grown during the past years and now a portion of the yield generated every month is passed to the NFT owners.

This is done trough a contract called “The Locker”. Every NFT that are in the locker at the time of the monthly distribution will receive an ecual portion of it. Llama in the locker can only be pulled out during a 7 days period every 28 days.

This design has two main impact on the collection:

- Llama are yield bearing assets, they magicaly make money on their own
- This has greatly diminished the amount of NFT from the collection listed on exchange platform (19 at the time of writing, slightly up from ATL due to OPEN snapshot) as peoples seems to quite like the deal of getting $40 a month for some restriction on liquidity

### Impact on NFTStrategy

Those features allow us to explore a totaly different design space than the original as we don't need to rely on external factor to generate money to sustain the flywheel. By simply locking the NFT the Strategy can be self suficient. futhermore due to the low liquidity mentioned earlier it seems far easier to induce a supply crunch by locking llamas forever rather than relisting them at a higher price (which as far as I'm concerned a more important goals than allowing peoples to gamble on a memecoin with marginal utility).

### All llamas are 1/1



