# [WIP] Llama_Exchange_Stategy

___

/!\ This is an invite to participate in a game theory reflexion, and shouldn't be interpreted as financial advice.
___

## Abstract

NFTStrategies from Tokenwork have been picking up in popularity recently (with my writing speed the fad might be dead by the time you read this line). After a not so brief introduction to the subject we will discuss the specificity of The Llamas collection and how they can impact the working of the original design. This will be followed by the introduction of alternative designs that makes use of those specificity, how different token model could enhance it and the possible upsides and downsides. Finaly a section will be dedicated to some of the implementation details and possible hurdles.
___

## Introduction

### What's the Strategy ?

If you are familiar with Bitcoin you might have heard of [MicroStrategy](https://en.wikipedia.org/wiki/MicroStrategy) the company funded by Michael Sailor which is accumulating Bitcoin en masse. This is done by various way, including debt backed by convertible share (I will not pretend I know what it means). As the share price went up a lot, other company followed suite, using diverse means (debt, convertible or not, spare cash, etc) to acquire crypto (mainly bitcoin, ETH for some, and sometime SOL) and add it to their treasury. Those company are refered  as Digital Asset Treasury (abreviated DAT), but many adopted the word “Strategy" as part of their branding culminating with [MicroStrategy renaming as Strategy earlier this year](https://www.strategy.com/press/microstrategy-is-now-strategy_02-05-2025).

Comming back full circle DeFi protocols started to appear using the "Strategy" branding, some like [ETH Strategy](https://x.com/eth_strategy) taking the convertible share concept to the letter, other taking more liberties. The one of interest for today, [TokenWorks](https://x.com/token_works)'s product: NFTStrategy is on the looser side.

### NFTStrategy

Starting with the CryptoPunks collection in early september the design was as follow (this is a simplified explanation, some fee are redirected to the team, etc):

1. Create a token and put all the liquidity in a token/ETH pool on UNIv4 with a 10% fee
2. As peoples buy the token the protocol who own a huge chunk of the supply of token will start to accrue fee in ETH
3. Those fees are than used to buy an NFT from the collection
4. The NFT is then relisted at 1.2 times the price it was bought at
5. When said NFT is sold the proceed of the sale is used to buy back and burn the token from step 1. This provide the incentive for people to buy the taoken in step 2, sustaining the flywheel.

This initial attemp was met with sucess leading to the creation of spin-off for various other collection and ERC20 by the original teami (funelling a part of the fee into the original punk strategy and the collection owner), but also by other team [with various degree of success](https://x.com/0xz80/status/1972731977355698452). You can even find a Strategy accumulating the cryptopunk strategy token, and another one accumulating the token of the strategy accumulating token from PunkStrategy.

### The Llamas

[The Llamas](https://x.com/WenLlama) is an NFT collection with 1111 token, but unlike most collection the money raised trough the sell in an auction have been used to create a treasury, mainly centered around the [Curve](https://x.com/CurveFinance) ecosystem, this treasury has been grown during the past years and now a portion of the yield generated every month is passed to the NFT owners.

This is done trough a contract called [The Locker](https://locker.thellamas.io/). Every NFT that are in the locker at the time of the monthly distribution will receive an equal portion of it. Llamas in the locker can only be pulled out during a 7 days period every 28 days.

This design has two main impact on the collection:

- Llama are yield generating assets, they magicaly make money on their own
- This has greatly diminished the amount of NFT from the collection listed on exchange platform (19 at the time of writing, slightly up from ATL due to OPEN snapshot) as peoples seems to quite like the deal of getting $40 (or 25$ during uptober) a month for some restriction on liquidity.

## Impact on a potential Strategy

Those features allow us to explore a totaly different design space than the original as we don't need to rely on external factor to generate money to sustain the flywheel. By simply locking the NFT the protocol can be self suficient. futhermore due to the low liquidity mentioned earlier it seems far easier to induce a supply crunch by locking llamas forever rather than relisting them at a higher price (which as far as I'm concerned a more important goals than allowing peoples to gamble on a memecoin with marginal utility).

### Drawbacks

Before exploring this design space it seems important to me to stop and discuss the potential drawbacks of locking llama forever and how to address them.

- All Llamas are 1/1, This means some design would become unavailable forever. However this can be an oportunity for extra cashflow, by allowing peoples to exchange a llama in the protocol for another one for a fee.
- Yield dilution. The more Llamas are locked in the locker the lesser your share of the reward from the monthly distribution. However this effect would not be that big in today's context. Currently 720 llamas are in the locker, add that another 135 are currently in the treasury and thus not lockable (or we revolt), this leave only 256 llamas in the wild, if they were to be all locked this would lead to a maximum of around 26% of dilution.
- The locker, while being quite close to an immutable contract, the distribution of the yield is very much a ruggable process, should the collection stop the yield distribution or change the contract that get said yield. The protocol would hence need to have a way to wind down or mutate, either automaticaly, through governance or even just giving the key to the treasury.

### Design

#### No token

Thanks to the yield from the locker the protocol doesn't NEED a token. By funelling the yield into buying more llamas the protocol can grow it's inventory exponentialy. This however would suffer from an absolute zero cold start, needing dozen of years for the yield of one llama to buy a second one, assuming the past yield represent future performance and llama price wouldn't change, and that's still assuming you are starting with 1 llama, while under those assumption a minimum of 10 Llamas would be needed to see an effect on floor price in ones lifespan.

#### The purrfect one

Don't hesitate to share your view.

